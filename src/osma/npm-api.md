---
label: NPM API
icon: package-dependencies
order: 530
---

# NPM API

**Base URL:** `https://notamitgamer-osma-npm-api.hf.space`

## GET /ping

Uptime check — always returns 200. Lightweight endpoint for UptimeRobot or health monitors; doesn't query the database.

```bash
curl https://notamitgamer-osma-npm-api.hf.space/ping
```

```json
{ "ping": "pong" }
```

## GET /health

Server status + total package count. Returns `200` with the package count once the database is ready; returns `503` if it's still initializing after a cold start.

```bash
curl https://notamitgamer-osma-npm-api.hf.space/health
```

```json
{
  "status": "ok",
  "total_packages": 3881465
}
```

## GET /stats

Dataset metadata and package count, intended for dashboard stats bars.

```bash
curl https://notamitgamer-osma-npm-api.hf.space/stats
```

```json
{
  "total_npm_packages": 3881465,
  "source": "npmjs.com",
  "note": "Snapshot dataset — updated periodically."
}
```

## GET /browse

Paginated package list, ordered by `package_no`.

| Parameter | Type | Default | Max | Required | Description |
|---|---|---|---|---|---|
| `page` | integer | 1 | — | optional | Page number, 1-indexed |
| `limit` | integer | 200 | 500 | optional | Rows per page |

```bash
curl "https://notamitgamer-osma-npm-api.hf.space/browse?page=1&limit=5"
```

```json
{
  "page": 1,
  "limit": 5,
  "results": [
    { "no": 1, "name": "--123hoodmane-pyodide", "version": "latest", "url": "https://www.npmjs.com/package/..." }
  ]
}
```

## GET /search

Ranked search across all packages. Results are ranked by match quality — exact match (`0`) first, starts-with (`1`) second, contains (`2`) last — then sorted alphabetically within each rank.

| Parameter | Type | Default | Max | Required | Description |
|---|---|---|---|---|---|
| `q` | string | — | 100 chars | required | Search query, min 2 characters |
| `limit` | integer | 250 | 500 | optional | Max results to return |

```bash
curl "https://notamitgamer-osma-npm-api.hf.space/search?q=react&limit=5"
```

```json
{
  "query": "react",
  "count": 250,
  "results": [
    { "no": 42, "name": "react", "version": "18.3.1", "url": "...", "rank": 0 },
    { "no": 88, "name": "react-dom", "version": "18.3.1", "url": "...", "rank": 1 }
  ]
}
```
