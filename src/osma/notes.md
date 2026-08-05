---
label: Notes & FAQ
icon: question
order: 500
---

# Notes & Reference

## Limits & notes

**Rate limits** — APIs are strictly rate-limited to 10 requests/minute and 100 requests/hour per IP to protect the free-tier infrastructure. Send the `X-Bypass-Token` header to override this.

**Data freshness** — both datasets are snapshots. NPM was frozen `2026-04-29 09:42 IST`, PyPI `2026-04-29 08:45 IST`. Packages published after these dates aren't indexed.

**CORS** — both APIs have `Access-Control-Allow-Origin: *`, so you can call them directly from any browser-based frontend with no proxy needed.

**Cold starts** — on first boot after a deployment, each server downloads its dataset and builds a SQLite index (~1 min). `/health` returns `503` during this window. UptimeRobot prevents this in normal operation.

## Response schema

`results` arrays from `/browse` or `/search` contain objects with:

| Field | Type | Description |
|---|---|---|
| `no` | integer | Stable, sequential ID/rank of the package within the snapshot database |
| `name` | string | The exact, registered name of the package |
| `version` | string | Version string available at the time the snapshot was taken |
| `url` | string | Absolute link to the package on the official registry website |
| `rank` | integer | *(`/search` only)* Match quality: `0` exact, `1` starts-with, `2` contains |

## Common errors

**`404` Not Found** — the API URL path is incorrect or misspelled (e.g. `/searc` instead of `/search`).

**`422` Unprocessable Entity** — `/search` was called without the required `q` parameter, or the query was under 2 characters.

**`429` Too Many Requests** — you exceeded the 10/min or 100/hour rate limit. The response includes a `Retry-After` header.

**`503` Service Unavailable** — the server was asleep (cold start) and is downloading the dataset / building its SQLite index. Normal on free-tier hosting; usually resolves within a minute.

!!!warning Still having trouble?
If you're seeing continuous `500` errors or found a bug, [open an issue on GitHub](https://github.com/notamitgamer/osma/issues) or email [mail@amit.is-a.dev](mailto:mail@amit.is-a.dev).
!!!

## FAQ

**What exactly is OSMA?**
A heavily optimized, static API serving historical snapshots of the NPM and PyPI registries — search packages and view base version data instantly without live registry rate limits or CAPTCHAs.

**Why can't I find a recently published package?**
The datasets are frozen snapshots from April 29, 2026. Anything published, renamed, or deleted after that date won't appear.

**Is there rate limiting?**
Yes — 10 requests/minute and 100/hour per IP via SlowAPI. Open a GitHub issue to request an `X-Bypass-Token` if you need it disabled.

**Do I need an API key?**
No — the APIs are fully open and require no authentication for standard usage within the rate limits.

**Can I use this in a frontend app directly?**
Yes — both APIs have open CORS (`Access-Control-Allow-Origin: *`), so browser apps can fetch directly with no proxy.

**What does the `rank` field mean?**
`0` = exact match, `1` = starts with the query, `2` = contains the query somewhere in the name.

**Why does `/health` sometimes return 503?**
The server went to sleep from inactivity. On waking (a "cold start") it needs 1–2 minutes to download the CSV snapshot and rebuild its index — it returns `503` while loading.

**How many packages are indexed?**
Roughly 3.88 million NPM packages and 793,000 PyPI packages as of the current snapshots. Check `/stats` for exact live numbers.

**Are other registries (RubyGems, Cargo) planned?**
The current focus is strictly NPM and PyPI; other ecosystems may be considered with enough demand.

**How do I report a bug or vulnerability?**
General bugs/UI issues → [open a GitHub issue](https://github.com/notamitgamer/osma/issues). Security vulnerabilities → email [mail@amit.is-a.dev](mailto:mail@amit.is-a.dev) directly instead of filing a public issue.
