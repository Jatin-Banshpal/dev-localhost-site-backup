# dev.localhost — Frappe site backup

Full backup of the `dev.localhost` site from the frappe-bench, taken **2026-09-01** with `bench backup --with-files`.

| File | Contents |
|---|---|
| `*-database.sql.gz` | MariaDB database dump |
| `*-files.tar` | Public files (`sites/dev.localhost/public/files`) |
| `*-private-files.tar` | Private files (`sites/dev.localhost/private/files`) |
> ⚠️ The `site_config_backup.json` produced by `bench backup` is deliberately **not** committed — it contains credentials (admin/DB passwords, and the `encryption_key` needed to restore encrypted fields). It is kept only on the bench at `sites/dev.localhost/private/backups/` and in the local copy of this repo; store the encryption key in a password manager.

## Restore

```bash
bench --site <site-name> restore \
  20260901_195945-dev_localhost-database.sql.gz \
  --with-public-files 20260901_195945-dev_localhost-files.tar \
  --with-private-files 20260901_195945-dev_localhost-private-files.tar
```

Then copy the `encryption_key` from `site_config_backup.json` into the restored site's `site_config.json`.
