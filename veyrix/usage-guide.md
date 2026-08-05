# Comprehensive Usage Guide

How to operate Veyrix IDE effectively — file management, keyboard shortcuts, versioning, and sharing.

## 1. Managing files

**Creating a new file** — click the `+` icon in the sidebar (or the floating button on mobile). Type your desired filename including the extension (e.g. `script.js`, `index.html`, `Dockerfile`). Veyrix auto-detects the language from the extension for syntax highlighting. Files without an extension are allowed.

**Importing an existing file** — click the Open File icon (folder with up arrow) in the top navigation bar, or press `Ctrl+O`. Select any valid text, configuration, or code file. Binary files (images, compiled `.exe` files) are rejected.

**Renaming or deleting** — hover over any file in the left sidebar and click the three-dots (`...`) icon. From the dropdown: Rename, Delete, or Download that specific file.

## 2. Editing & formatting

**Autosave & manual save** — Veyrix caches your typing to the local database 500ms after you stop typing. A blue dot next to the filename in the top bar indicates unsaved changes. Force a save any time with `Ctrl+S` or the floppy disk icon.

**Code formatting (Prettier)** — press `Alt+Shift+F` to beautify code (fix indentation and spacing). Only supported for recognized web languages: HTML, CSS, JS/JSX, JSON, Markdown.

## 3. Snapshots (local version history)

Veyrix has a built-in "Time Machine" for your files.

- **Save a snapshot** — click the bookmark icon top right; saves a frozen copy of your code at that moment
- **Limits** — max 5 snapshots per file; saving a 6th prompts you to permanently delete the oldest one
- **Restore** — click the clock icon to view history; clicking "Restore" on an older version immediately replaces your current editor content with the historical code

## 4. Sharing code

Click the Share icon to open the sharing modal. Three options:

**Fast local share** — compresses your entire file into the URL; no data leaves your browser. Best for small snippets, since large files produce very long URLs.

**Cloud share** — uploads your code to an anonymous, secure Firebase database and generates a short link. Can optionally be protected with a password (hashed client-side — see [Security & Threat Model](security.md)).

**Share via device** — uses your phone or computer's native share menu (AirDrop, WhatsApp, Email, etc.) to send the raw text of your code.
