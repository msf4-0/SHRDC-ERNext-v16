# SHRDC ERPNext v16

Custom ERPNext v16 with all SHRDC apps pre-installed. Single-command deployment.

## Requirements

- Docker (20.10+) and Docker Compose
- 4 GB RAM minimum, 8 GB recommended

## Quick Start

```bash
git clone https://github.com/msf4-0/SHRDC-ERNext-v16
cd SHRDC-ERNext-v16
docker compose -f shrdc-compose.yml up -d
```

Wait for the site to be created:

```bash
docker compose -f shrdc-compose.yml logs create-site -f
```

Once complete (5-10 min), access at **http://localhost:8080**

- **Username:** Administrator
- **Password:** admin

## Apps Included

| App | Purpose |
|---|---|
| ERPNext | Core ERP system (v16) |
| Autocount | Accounting integration |
| Short Courses | Training management |
| Frepple | Production planning |
| Barcode SHRDC | Barcode scanning |
| Telegram Integration | Telegram messaging |
| HRMS | HR management |
| Metabase Integration | Analytics integration |
| Shopify | E-commerce integration |
| SQL Accounting | SQL accounting software |
| E Invoice ERP | E-invoicing (LHDN) |

## Update

When a new image version is released, update without data loss:

```bash
cd shrdc-erpnext
docker compose -f shrdc-compose.yml pull
docker compose -f shrdc-compose.yml up -d
```

The `create-site` service detects the site already exists and exits. All other services (backend, frontend, workers, queues, scheduler) restart with the new image. **All data in the database and site files is preserved.**

### Sync Workspace & Fixture Changes

If the update includes new workspaces (like autocount icon or e_invoice_erp workspace), run:

```bash
docker compose -f shrdc-compose.yml exec backend bench --site frontend migrate
```

This applies any workspace JSON, custom field, or fixture changes to the existing site without data loss.

### Backup Before Update (Recommended)

```bash
docker compose -f shrdc-compose.yml exec backend bench --site frontend backup
```

Backups are stored in `sites/frontend/private/backups/` inside the Docker volume.

## Custom Port

If port 8080 is in use, edit `shrdc-erpnext/shrdc-compose.yml` and change:

```yaml
    ports:
      - "8081:8080"
```

Then access at http://localhost:8081.

## Stop

```bash
cd shrdc-erpnext
docker compose -f shrdc-compose.yml down
```

To remove all data:

```bash
cd shrdc-erpnext
docker compose -f shrdc-compose.yml down -v
```
