# Installation

```bash
pip install githrun
```

# Run Remote Code

Execute a script directly from a URL.

## Basic execution

```bash
githrun run https://github.com/user/repo/blob/main/script.py
```

## Run gists

```bash
githrun run https://gist.github.com/user/1234567890abcdef
```

## Auto-install dependencies

If a remote script needs packages you don't have (e.g. pandas, requests), run it in an isolated environment:

```bash
githrun run https://github.com/user/repo/blob/main/data.py --auto-install
```

## Inspect before running

View the source with syntax highlighting before executing it — a safety check:

```bash
githrun run https://github.com/user/repo/blob/main/script.py --inspect
```

Continue to [Auth, Bookmarks & Tool Install](cli-auth-and-tools.md).
