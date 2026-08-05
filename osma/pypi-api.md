# PyPI API

**Base URL:** `https://notamitgamer-osma-pypi-api.hf.space`

## GET /ping

Uptime check — always returns 200. Lightweight endpoint for UptimeRobot or health monitors; doesn't query the database.

```bash
curl https://notamitgamer-osma-pypi-api.hf.space/ping
```

```json
{ "ping": "pong" }
```

## GET /health

Server status + total package count. Returns `200` when the database is ready; returns `503` during cold-start initialization.

```bash
curl https://notamitgamer-osma-pypi-api.hf.space/health
```

```json
{
  "status": "ok",
  "total_packages": 780432
}
```

## GET /stats

Total package count and dataset source metadata.

```bash
curl https://notamitgamer-osma-pypi-api.hf.space/stats
```

```json
{
  "total_pypi_packages": 780432,
  "source": "pypi.org",
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
curl "https://notamitgamer-osma-pypi-api.hf.space/browse?page=1&limit=5"
```

```json
{
  "page": 1,
  "limit": 5,
  "results": [
    { "no": 1, "name": "0", "version": "0.1.0", "url": "https://pypi.org/project/0/" }
  ]
}
```

## GET /search

Ranked search across all packages. `0` = exact match, `1` = starts-with, `2` = contains.

| Parameter | Type | Default | Max | Required | Description |
|---|---|---|---|---|---|
| `q` | string | — | 100 chars | required | Search query, min 2 characters |
| `limit` | integer | 250 | 500 | optional | Max results to return |

```bash
curl "https://notamitgamer-osma-pypi-api.hf.space/search?q=requests&limit=5"
```

```json
{
  "query": "requests",
  "count": 87,
  "results": [
    { "no": 512, "name": "requests", "version": "2.31.0", "url": "...", "rank": 0 }
  ]
}
```
