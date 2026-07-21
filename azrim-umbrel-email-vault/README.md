# azrim-umbrel-email-vault

Umbrel Community App: **Email Vault** — manage catch-all aliases + find mail in Gmail vault.

- Server: https://github.com/azrim/email-vault-panel
- Image: `ghcr.io/azrim/email-vault-panel:0.1.0`

## Status

- [x] Store packaging
- [x] Phase 1 aliases (generate / list / archive)
- [x] Image on GHCR (public)
- [ ] Gmail phase 2
- [ ] Confirmed install open on umbrelOS

## If stuck on "Starting"

1. Refresh community store (`azrim/azrim_umbrel`)
2. Update app to **0.1.1** (or uninstall → install)
3. On host (Settings → Terminal → **umbrelOS**, not Hermes):

```bash
docker ps -a | grep -i email-vault
docker logs azrim-umbrel-email-vault_server_1 --tail 80
docker logs azrim-umbrel-email-vault_app_proxy_1 --tail 80
```

Common causes: wrong `APP_HOST`, image pull fail, proxy auth health hang.

## Pattern

`app_proxy` + `server`, data under `${APP_DATA_DIR}/data`.
