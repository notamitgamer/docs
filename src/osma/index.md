---
label: OSMA
icon: package
order: 550
---

# OSMA (Open Source Module Archive)

**Registry lookups, without the wait.** OSMA is a lightning-fast, static search archive for querying open-source packages across NPM and PyPI, bypassing live registry bottlenecks.

## Why it exists

Looking up package details on the official registries usually means dealing with:

1. **Fastly security checks** — CAPTCHAs or verification screens just to view a text page
2. **The multi-click tax** — clicking through 2-3 pages just to find a version tag or repo link

**The fix:** complete static snapshots of both registries were taken — **NPM at 2026-04-29 09:42 IST**, **PyPI at 2026-04-29 08:45 IST** — and indexed into a custom backend. This lets you instantly search and verify packages without ever hitting a live registry rate limit. Clicking a package in the UI still fetches its extended live details securely via a side-panel.

## Live explorers & docs

- **Home:** [data.amit.is-a.dev](https://data.amit.is-a.dev)
- **NPM Explorer:** [data.amit.is-a.dev/npm](https://data.amit.is-a.dev/npm)
- **PyPI Explorer:** [data.amit.is-a.dev/pypi](https://data.amit.is-a.dev/pypi)
- **API Docs (live):** [data.amit.is-a.dev/docs](https://data.amit.is-a.dev/docs)

## How the backend works

The backend runs on **FastAPI**, serving static `.csv` snapshots pulled securely from HuggingFace datasets.

- **SQLite indexing** — on first boot, the server downloads the multi-gigabyte dataset and builds an optimized, indexed SQLite database (WAL mode)
- **Speed** — because the dataset is localized, `/search` and `/browse` respond in milliseconds
- **Rate limiting** — strict limits (10 requests/minute, 100/hour) protect the free-tier infrastructure, enforced via `slowapi`; developers can request an `X-Bypass-Token` via a GitHub issue
- **Ranking logic** — search results are ranked `0` exact match → `1` starts with query → `2` contains query
- **Limitation** — as a frozen archive, packages published or deleted after April 2026 aren't indexed

## Get started

- [Quick Start](quickstart.md)
- [NPM API Reference](npm-api.md)
- [PyPI API Reference](pypi-api.md)
- [Utility Endpoints](utility.md)
- [Notes, Limits & FAQ](notes.md)
