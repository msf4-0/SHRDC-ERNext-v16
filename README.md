# SHRDC ERPNext v15

Custom ERPNext v15 with all SHRDC apps pre-installed. Single-command deployment.

## Requirements

- Docker (20.10+) and Docker Compose
- 4 GB RAM minimum, 8 GB recommended

## Quick Start

```bash
git clone https://github.com/msf4-0/SHRDC-ERNext-v15.git
cd SHRDC-ERNext-v15
docker compose -f shrdc-compose.yml up -d
```

Wait for the site to be created:

```bash
cd SHRDC-ERNext-v15
docker compose -f shrdc-compose.yml logs create-site -f
```

Once complete (5-10 min), access at **http://localhost:8080**

- **Username:** Administrator
- **Password:** admin

## Apps Included

| App | Purpose |
|---|---|
| ERPNext | Core ERP system (v15) |
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
cd SHRDC-ERNext-v15
docker compose -f shrdc-compose.yml pull
docker compose -f shrdc-compose.yml up -d
```

The `create-site` service detects the site already exists and exits. All other services restart with the new image. **All data is preserved.**

### Sync Workspace & Fixture Changes

```bash
docker compose -f shrdc-compose.yml exec backend bench --site frontend migrate
```

### Backup Before Update (Recommended)

```bash
docker compose -f shrdc-compose.yml exec backend bench --site frontend backup
```

## Custom Port

If port 8080 is in use, edit `SHRDC-ERNext-v15/shrdc-compose.yml` and change:

```yaml
    ports:
      - "8081:8080"
```

Then access at http://localhost:8081.

## Stop

```bash
cd SHRDC-ERNext-v15
docker compose -f shrdc-compose.yml down
```

To remove all data:

```bash
cd SHRDC-ERNext-v15
docker compose -f shrdc-compose.yml down -v
```
