---
label: CLI - Auth, Bookmarks & Tools
order: 680
---

# Authentication (Private Repos & Rate Limits)

GitHub limits unauthenticated requests to 60/hour. Logging in raises this to 5,000 and grants access to private repositories.

```bash
githrun login ghp_YourPersonalAccessToken...
```

The token is stored securely in `~/.githrun/config.json`.

# Bookmarks

Stop copy-pasting long URLs — save them once, run them anywhere.

```bash
# Add a bookmark
githrun bookmark add clean-db https://github.com/user/repo/blob/main/utils/cleanup.py

# Run a bookmark
githrun run clean-db

# List bookmarks
githrun bookmark list
```

# Install as a Tool

Turn a remote Python script into a command you can run from anywhere in your terminal.

```bash
githrun install https://github.com/user/repo/blob/main/my-tool.py --name mytool
```

- **Windows** — creates a `.bat` file in `~/.githrun/bin`
- **Linux/Mac** — creates an executable shim in `~/.githrun/bin`

!!!warning
You must add `~/.githrun/bin` to your system PATH for installed tools to be runnable directly.
!!!

Continue to [Find, Search & Download](cli-find-download.md).
