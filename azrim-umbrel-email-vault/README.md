# azrim-umbrel-email-vault

Umbrel Community App: **Email Vault** — manage catch-all aliases + find mail in Gmail vault.

Spec: see Hermes durable notes  
`/opt/data/projects/email-pool/EMAIL_VAULT_PANEL_SPEC.md`  
(or mirror into this folder when the server repo is split).

## Status

- [x] Store skeleton (`umbrel-app.yml`, `docker-compose.yml`)
- [x] Panel server phase 1 source: `https://github.com/azrim/email-vault-panel`
- [x] Image `ghcr.io/azrim/email-vault-panel:0.1.0` (+ `latest`)
- [ ] Gmail OAuth (phase 2)
- [ ] Install smoke on umbrelOS

Install after Community Store refresh. First open = alias manager only (no Gmail yet).

## Pattern

Same as sibling apps: `app_proxy` + one `server` service, data under `${APP_DATA_DIR}/data`.
