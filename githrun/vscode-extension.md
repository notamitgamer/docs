# VS Code Extension

## Installation & setup

### 1. Install the extension

- **Marketplace** — search for "Githrun" in the VS Code Extensions view and click Install
- **Manual** — if installing from a VSIX file, go to Extensions → **...** → Install from VSIX

### 2. Install the core CLI (required)

The extension acts as a bridge to the Githrun CLI — you must have it installed on your system:

```bash
pip install githrun
```

## Extension features & usage

### CodeLens integration

The extension automatically scans Markdown, Python, and Text files for GitHub or Gist URLs. Look for the "Run with Githrun" link appearing above any detected URL — click it to open a terminal and run the script immediately.

### Context menu

Highlight any GitHub URL in your editor, right-click the selection, and choose **Githrun: Run Selected Text**.

### Command palette

Press `Ctrl+Shift+P` (or `Cmd+Shift+P` on Mac), type `Githrun: Run from URL...`, and paste your target link.

## Extension settings

The extension tries to auto-detect your Githrun installation:

1. First checks for `githrun` in your global PATH
2. If not found, falls back to `python -m githrun` (or `python3` on Mac/Linux)

Continue to [Configuration](configuration.md).
