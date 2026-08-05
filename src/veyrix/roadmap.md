---
label: Limitations & Roadmap
icon: milestone
order: 540
---

# Current Limitations

- **Flat file system** — the main IDE has no directory/subfolder support; flat array mapping only (Veyrix Web solves this separately with a true VFS)
- **Snapshot limit** — hardcoded FIFO limit of 5 snapshots per file, to prevent storage quota bloat
- **No language servers** — relies entirely on basic Ace autocompletion arrays; no deep IntelliSense (LSP)
- **Single view** — split-pane or multi-tab rendering isn't yet supported in the main IDE's DOM structure

# Development Roadmap

## Core IDE

**v1.1.0** — Removed the Ace.js worker to reduce RAM usage.

**v1.0.9** — Re-engineered the file sharing logic to use `application/octet-stream` and URI-context anchoring, bypassing strict Desktop OS security blocks that previously triggered "Permission Denied" errors.

**v1.0.8** — Updated version history logic to trigger a confirmation modal before restoration, preventing accidental data loss and ensuring a clean editor state after recovery.

## Web IDE

**v1.0.2** — Implemented a draggable split-pane interface (Dynamic Viewport Resizer), letting users manually adjust preview width to simulate and test designs across device breakpoints.

**v1.0.1** — Introduced nested folder mapping, batch file uploads, and a persistence-linked tab system for navigating complex project structures (Advanced File System & Workspace).
