# azrim-umbrel-9router

Umbrel Community App packaging for [decolua/9router](https://github.com/decolua/9router).

## Install (umbrelOS)

1. App Store → Community → ensure store  
   `https://github.com/azrim/azrim_umbrel` is added.
2. Refresh / reopen Community store → install **9Router**.
3. Open from homescreen → set dashboard password if prompted.
4. OpenAI API: same app URL + path `/v1` with an API key created in 9Router Settings.

## Data

Persists under the app data dir → `/app/data` (sqlite, auth, providers).

## Farm / Hermes notes

- Browser account farm stays on **azrim VPS**; this app is for **Umbrel UI + local routing**.
- Import farm `grok-web` SSO cookies after install (see Hermes `email-pool/NINE_ROUTER.md`).
- If the app stays on “Starting”, check container logs on the Umbrel host; try `APP_HOST: server` in compose if your OS version expects short service names.

## Image

`decolua/9router:latest` (public Docker Hub).
