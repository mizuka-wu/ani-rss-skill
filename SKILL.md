# ani-rss

Manage anime RSS subscriptions via [ani-rss](https://github.com/wushuo894/ani-rss). Use when the user wants to list, add, delete, search, or manage anime subscriptions, or interact with the ani-rss server.

## Setup

First configure the server URL and auth:

```bash
# API key auth (recommended)
bash scripts/ani-rss.sh config set --url http://localhost:12444 --api-key <api-key>

# Or JWT auth (login with credentials)
bash scripts/ani-rss.sh config set --url http://localhost:12444
bash scripts/ani-rss.sh login --username admin --password admin
```

Config stored at `~/.config/ani-rss/config.json`. Override with `ANI_RSS_URL` / `ANI_RSS_API_KEY` env vars.

## Script

All interactions go through `scripts/ani-rss.sh` (relative to this skill directory). All output is JSON. Errors to stderr, non-zero exit on failure.

## Workflow

### Browse & search

```bash
bash scripts/ani-rss.sh list
bash scripts/ani-rss.sh search-bgm "孤独摇滚"
bash scripts/ani-rss.sh bgm-to-ani 395855
bash scripts/ani-rss.sh mikan "孤独摇滚"
bash scripts/ani-rss.sh mikan-group "https://mikanani.me/Bangumi/xxx"
```

### Add subscription

1. Search: `bash scripts/ani-rss.sh search-bgm "<name>"`
2. Get Ani object: `bash scripts/ani-rss.sh bgm-to-ani <subject-id>`
3. Modify as needed, then add: `bash scripts/ani-rss.sh add '<json>'`

Or from RSS URL:
```bash
bash scripts/ani-rss.sh add '{"url":"https://mikanani.me/RSS/Bangumi?bangumiId=123&subgroupid=456","title":"Example"}'
```

### Manage

```bash
bash scripts/ani-rss.sh list
bash scripts/ani-rss.sh refresh            # all
bash scripts/ani-rss.sh refresh <id>       # one
bash scripts/ani-rss.sh enable '["id1"]'
bash scripts/ani-rss.sh disable '["id1"]'
bash scripts/ani-rss.sh delete '["id1"]' true
bash scripts/ani-rss.sh set '{"id":"xxx",...}'
```

### Server

```bash
bash scripts/ani-rss.sh ping
bash scripts/ani-rss.sh about
bash scripts/ani-rss.sh config-get
bash scripts/ani-rss.sh logs
bash scripts/ani-rss.sh clear-cache
```

### Raw API

```bash
bash scripts/ani-rss.sh raw /endpoint POST '{"k":"v"}' "param=val"
```

## Auth

| Method | Header | Notes |
|--------|--------|-------|
| API Key | `x-api-key` | Recommended, no expiry |
| JWT | `Authorization` | Login via `/login`, password is MD5 |

## API reference

| Endpoint | Description |
|----------|-------------|
| `GET /ping` | Health check |
| `POST /login` | Login (body: `{username, password}`) |
| `POST /listAni` | List subscriptions |
| `POST /addAni` | Add subscription |
| `POST /setAni` | Update subscription |
| `POST /deleteAni` | Delete (body: ids[], ?deleteFiles) |
| `POST /refreshAll` | Refresh all RSS |
| `POST /refreshAni` | Refresh one (body: {id}) |
| `POST /batchEnable` | Enable/disable (body: ids[], ?value) |
| `POST /searchBgm?name=` | Search Bangumi |
| `POST /getAniBySubjectId?id=` | BGM → Ani |
| `POST /config` | Get server config |
| `POST /setConfig` | Update config |
| `POST /scrape` | Scrape metadata |
| `POST /batchScrape` | Batch scrape (body: ids[]) |
| `POST /logs` | Get logs |
| `POST /about` | Version info |
| `POST /mikan?text=` | Search Mikan |
| `POST /animeGardenList` | AnimeGarden list |
