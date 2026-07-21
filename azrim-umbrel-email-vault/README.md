# azrim-umbrel-email-vault

Umbrel Community App: **Email Vault** — manage catch-all aliases + find mail in Gmail vault.

Spec: see Hermes durable notes  
`/opt/data/projects/email-pool/EMAIL_VAULT_PANEL_SPEC.md`  
(or mirror into this folder when the server repo is split).

## Status

- [x] Store skeleton (`umbrel-app.yml`, `docker-compose.yml`)
- [x] Panel server phase 1 source: `azrim/email-vault-panel` (aliases CRUD)
- [ ] Published image `ghcr.io/azrim/email-vault-panel:0.1.0` (build on host with Docker)
- [ ] Gmail OAuth (phase 2)
- [ ] Install smoke on umbrelOS

Do not install from store until the image is published (or compose points at a local build).

## Pattern

Same as sibling apps: `app_proxy` + one `server` service, data under `${APP_DATA_DIR}/data`.
