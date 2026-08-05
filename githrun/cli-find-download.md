# Find & Search

Search for files inside a remote repository without cloning it.

```bash
# Search for files containing "config"
githrun find https://github.com/user/repo "config"
```

This command is interactive — you can select a result number to run it immediately.

# Download Files & Folders

## Download a single file

```bash
githrun download https://github.com/user/repo/blob/main/script.py
```

## Download a specific folder (recursive)

```bash
githrun download https://github.com/user/repo/tree/main/src/utils --output ./local_utils
```

# Show Folder Contents

List files in a remote directory to understand the structure:

```bash
githrun show https://github.com/user/repo/tree/main/src
```

Continue to [Python API](python-api.md).
