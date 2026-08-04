Script that downloads [APOD](https://apod.nasa.gov/apod/astropix.html) photos and sets them to my background

## Setup

Requires:

- [`jq`](https://jqlang.github.io/jq/) (`brew install jq`) for parsing the API response
- [`dotenvx`](https://dotenvx.com) (`brew install dotenvx/brew/dotenvx`) for loading `.env`

The script needs two env vars, set in `.env`:

- `APOD_API_KEY` — a NASA API key from https://api.nasa.gov (or `DEMO_KEY`)
- `IMAGE_DIR` — folder where images/json get saved (e.g. `/Users/evan/apod/images`)

## Running manually

```
dotenvx run -- ./apod
```

## Running on a cron

Add a line like this via `crontab -e`:

```
0 * * * * cd /Users/evan/apod && /opt/homebrew/bin/dotenvx run -- ./apod > apod.log 2>&1
```

Notes:

- `cron` runs with a minimal `PATH` so we need to call `dotenvx` with its full location
- Old images/json older than 30 days are cleaned up automatically by the script.
