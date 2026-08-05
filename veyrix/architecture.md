# Architecture & State Management

## Visual system design

Data flows through three strictly isolated layers:

- **Presentation layer** — Ace Editor & vanilla DOM UI, reading via `state.editor.getValue()`
- **Local persistence** — IndexedDB (`VeyrixFS`), written via `DB.save(state.files)`
- **Cloud share (lazy)** — Firebase Firestore, written via `addDoc(shared_snippets)` — only touched when the user explicitly shares to the cloud

## State management pattern

To maintain extreme performance on low-end mobile devices, Veyrix eschews frameworks like React or Vue. Instead it relies on a mutable, global singleton `state` object. UI updates happen through explicit imperative functions triggered by state mutations, avoiding full tree diffing.

```javascript
// Global State Singleton
const state = {
    files: [],              // Array of File objects
    activeFileId: null,     // ID of currently rendered file
    editor: null,           // Ace Editor instance reference
    db: null,               // IndexedDB connection instance
    renameTargetId: null    // Transient state for UI modals
};
```

**Architectural decision record (ADR):** the Ace Editor manages its own complex internal state (cursors, selections, undo stacks). Wrapping it in a reactive framework often causes race conditions during rapid typing. By keeping the source of truth in `state.editor` and extracting `value` asynchronously via debounced events, Veyrix achieves sub-16ms frame times.

## Local storage model (IndexedDB)

Persistence is managed entirely via the browser's native IndexedDB API through a Promisified wrapper. The database is named `VeyrixFS` (Version 1).

### Schema: `files` ObjectStore

KeyPath: `id`

```typescript
// TypeScript representation of the IndexedDB record
interface VeyrixFile {
  id: string;             // e.g., "f_a1b2c3d4e_1679000000"
  name: string;           // Base filename (e.g., "app")
  ext: string;            // Extension (e.g., "js", "html")
  content: string;        // Raw string payload of the editor
  unsaved: boolean;       // Tracks dirty state for the UI
  lastModified: number;   // Epoch timestamp
  snapshotCounter?: number;
  snapshots?: Snapshot[]; // Array (max length: 5, FIFO eviction)
}
```

## Cloud & synchronization strategy

Veyrix uses a zero-cost initial load strategy: Firebase SDKs (App, Auth, Firestore) are **not** bundled or loaded on startup. They're dynamically imported via ES Modules only when a user initiates a "Cloud Share."

### 1. Fast local share (LZ-String)

Compresses the payload with `LZString.compressToEncodedURIComponent`, yielding a base64-like URI-safe string appended directly to the URL. Entirely offline, entirely client-side.

### 2. Cloud share (Firestore)

Authenticates using `signInAnonymously()`, pushes the payload to the `shared_snippets` root collection, and returns a lightweight document ID reference in the URL.
