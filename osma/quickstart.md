# Quick Start

OSMA has fully open CORS and requires no authentication keys, so you can start fetching package data immediately — from a backend script, a CLI tool, or directly inside a browser application.

## JavaScript (browser & Node.js)

CORS is fully open (`Access-Control-Allow-Origin: *`), so you can use the native `fetch` API directly. This example queries the NPM snapshot for `react`:

```javascript
async function getPackageVersion(query) {
  const url = `https://notamitgamer-osma-npm-api.hf.space/search?q=${encodeURIComponent(query)}&limit=1`;

  try {
    const response = await fetch(url);
    if (!response.ok) throw new Error(`HTTP error! status: ${response.status}`);

    const data = await response.json();
    if (data.results && data.results.length > 0) {
      const pkg = data.results[0];
      console.log(`${pkg.name} | Version: ${pkg.version} | Rank: ${pkg.rank}`);
      console.log(`Registry Link: ${pkg.url}`);
    } else {
      console.log("Package not found in the April 2026 snapshot.");
    }
  } catch (error) {
    console.error("Failed to fetch OSMA data:", error);
  }
}

getPackageVersion("react");
```

## Python

For Python apps, tools, or data analysis scripts, `requests` makes querying the PyPI snapshot simple:

```python
import requests

def get_package_version(query):
    url = f"https://notamitgamer-osma-pypi-api.hf.space/search?q={query}&limit=1"
    try:
        response = requests.get(url)
        response.raise_for_status()
        data = response.json()

        if data.get("results"):
            pkg = data["results"][0]
            print(f"{pkg['name']} | Version: {pkg['version']} | Rank: {pkg['rank']}")
            print(f"Registry Link: {pkg['url']}")
        else:
            print("Package not found in the April 2026 snapshot.")

    except requests.exceptions.RequestException as e:
        print(f"Failed to fetch OSMA data: {e}")

if __name__ == "__main__":
    get_package_version("requests")
```

## Command line (cURL)

Fastest way to test an endpoint from your terminal:

```bash
curl -s "https://notamitgamer-osma-npm-api.hf.space/search?q=express&limit=3" | jq
```

!!!info Rate limits apply
These endpoints are subject to the standard free-tier rate limits (10 requests/minute, 100/hour). If you're writing a script that loops through hundreds of packages, you'll need an `X-Bypass-Token` — see [Utility Endpoints](utility.md).
!!!
