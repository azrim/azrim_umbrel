# azrim-umbrel-foxrouters

Umbrel Community App packaging for [FoxRouters](https://github.com/rilspratama/Foxrouters) v1.6.1.

**Why this instead of 9Router:** CodeBuddy **global** (`ck_*` API keys, `cb/*` models) is first-class here. 9Router is better for Claude/Codex/Grok-CLI multi-provider thrash — not CB global.

## Install (umbrelOS)

1. **Uninstall 9Router** (homescreen → right-click → Uninstall) if you are fully replacing it.  
   Optional: keep 9Router until FoxRouters is healthy (both can coexist; different ports).
2. App Store → Community → store `https://github.com/azrim/azrim_umbrel` → refresh.
3. Install **FoxRouters**.
4. Open from homescreen → `/login`.
5. Admin key (first boot):
   - App data: Files → Apps → FoxRouters → `data/foxrouters/gateway-key.txt`  
   - Or container logs: look for `AUTO-BOOTSTRAP` / Redis key `gw:key:gw-…`
6. Import CodeBuddy keys: Dashboard → Accounts → Bulk Import, or:

```bash
# From a machine that can reach the app (or Umbrel host)
curl -X POST http://<umbrel-host-or-tunnel>:20130/cb/import/bulk \
  -H "Authorization: Bearer $(cat gateway-key.txt)" \
  -H 'Content-Type: application/json' \
  -d @cb_import_bulk.json
```

7. Smoke:

```bash
curl -s http://127.0.0.1:20130/health
curl -s http://127.0.0.1:20130/v1/models -H "Authorization: Bearer $KEY"
curl -s http://127.0.0.1:20130/v1/chat/completions \
  -H "Authorization: Bearer $KEY" \
  -H 'Content-Type: application/json' \
  -d '{"model":"cb/gpt-5.5","messages":[{"role":"user","content":"ping"}]}'
```

## Hermes

- Old 9Router base (example): `http://10.21.0.1:20128/v1`
- FoxRouters base: **`http://10.21.0.1:20130/v1`** (after app is up; confirm Docker network reachability from Hermes)
- Use gateway admin/inference key from FoxRouters, not the old 9Router API key
- Models: `cb/gpt-5.5`, `cb/gpt-5.6-sol`, … and `grok-*` if you import Grok accounts

## Data

| Path (in app volume) | Role |
|----------------------|------|
| `data/redis/` | Redis AOF/RDB hot state (tokens, keys) |
| `data/foxrouters/` | SQLite logs + `gateway-key.txt` |

## Services

| Service | Image | Notes |
|---------|-------|--------|
| `server` | `ghcr.io/rilspratama/foxrouters:v1.6.1` | API + dashboard |
| `redis` | `redis:7-alpine` | Required hot state |

No ClickHouse (SQLite logs) — lighter for Umbrel 2C/4GB.

## Farm keys (azrim)

If you already farmed on azrim:

- Keys live in `azrim:~/codebuddy-farm/farm/results/batch_*/accounts.json`
- Or already imported on azrim FoxRouters: `~/foxrouters/cb_import_bulk.json`
- Copy bulk JSON to Umbrel and re-import (same API). Do **not** paste full keys into Telegram.

## Rollback

Reinstall **9Router** (`azrim-umbrel-9router`) from the same store if needed. FoxRouters data stays under its own app volume until you delete the app.
