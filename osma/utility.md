# Utility Endpoints

These endpoints are available on both the NPM and PyPI APIs. Examples below use the NPM base URL.

## GET /debug-ip

Returns the IP address the API proxy recorded for your request, along with parsed headers — useful for troubleshooting rate-limit blocks across networks.

```bash
curl https://notamitgamer-osma-npm-api.hf.space/debug-ip
```

## GET /get-bypass

Issues a cryptographically signed token that lets you skip all rate limits for 1 hour. Requires the correct `secret` parameter. Include the returned token on subsequent requests as the `X-Bypass-Token` header.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `secret` | string | required | The developer bypass secret |

```bash
curl "https://notamitgamer-osma-npm-api.hf.space/get-bypass?secret=YOUR_SECRET_HERE"
```

```json
{
  "bypass_token": "1714420000:a1b2c3d4...",
  "valid_for_seconds": 3600,
  "usage": "Send as header: X-Bypass-Token: <token>"
}
```

## GET /rebuild

Forces the server to re-download the latest CSV dataset from HuggingFace and rebuild the SQLite database in the background. Requires the `secret` parameter. Responds with `503` while rebuilding.
