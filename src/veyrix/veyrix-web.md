---
label: Veyrix Web (Multi-File)
icon: file-directory
order: 560
---

# Veyrix Web (Multi-File IDE)

Veyrix Web (`web.html`) is an advanced, multi-file environment built specifically for web development. Unlike the single-file main IDE, it uses a robust virtual file system with directory structures, multi-tab editing, and an integrated real-time preview window.

## Isolated database (VeyrixWebFS)

To prevent data collision with the main IDE, Veyrix Web uses a completely separate IndexedDB named `VeyrixWebFS`. It tracks full relative paths (e.g. `/css/style.css`) rather than flat IDs, enabling a true folder hierarchy.

```typescript
// VFS Node Representation
interface VFSNode {
  path: string;           // Absolute virtual path
  type: string;           // "file" or "folder"
  content: string;        // String payload or Base64 URI
  isBase64: boolean;      // Flags binary image assets
}
```

## Live preview engine

The core of the Web IDE is the `PreviewEngine`. Because all files live inside IndexedDB, standard relative HTML links (like `<link rel="stylesheet" href="style.css">`) fail natively inside an isolated iframe — the engine intercepts and resolves these on the fly.

**AST parsing & injection** — when rendering, the engine intercepts your `/index.html` file and uses the browser's native `DOMParser` API to scan the DOM for external scripts, styles, and image tags.

**Virtual path resolution** — using `PathUtils.resolve()`, it computes the absolute virtual path of each linked asset, retrieves its content from the VFS, and transforms it: `<link>` tags become inline `<style>` tags, and `<script src>` tags become inline execution blocks.

**Blob srcdoc rendering** — the compiled master HTML string is injected directly into the iframe's `srcdoc` attribute. This entirely bypasses cross-origin requests, eliminates network latency, and keeps processing fast and 100% offline.

## Workspace export (ZIP)

Unlike the main IDE (flat single files), Veyrix Web lets you export your entire workspace architecture.

- **Combine HTML** — leverages the PreviewEngine to bundle all CSS, JavaScript, and Base64 images into a single monolithic `index.html`. Good for quick sharing or embedding in systems that don't support multi-file directories.
- **ZIP archive export** — dynamically loads the `JSZip` library only when requested, maps over the virtual file system, constructs a standard directory structure, and outputs a downloadable `.zip` preserving all relative paths and binary formats.
