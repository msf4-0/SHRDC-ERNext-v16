# SHRDC v16 Image

Custom ERPNext v16 Docker image with all migrated apps pre-installed.

## Apps Included

| App | Source |
|---|---|---|
| ERPNext | frappe/erpnext (version-16) |
| Autocount | hisham733/autocount_v16 |
| Short Courses | hisham733/short_courses_v16 |
| Frepple | hisham733/frepple_v16 |
| Barcode SHRDC | hisham733/barcode_shrdc_v16 |
| Telegram Integration | hisham733/erpnext_telegram_integration_v16 |
| HRMS | hisham733/hrms_v16 |
| Metabase Integration | hisham733/metabase_integration_v16 |
| Shopify | hisham733/shopify_v16 |
| SQL Accounting Software | hisham733/sql_accounting_software_v16 |
| E Invoice ERP | hisham733/e_invoice_erp_v16 |

## Build the Image

This repo includes a GitHub Actions workflow that automatically builds and pushes the image when changes are pushed to `main`.

### Required Secret

Add a **Docker Hub access token** as a repository secret named `DOCKER_PAT`:

1. Go to https://hub.docker.com/settings/security
2. Create a new access token with Read & Write permissions
3. Add it to this repo: Settings → Secrets and variables → Actions → New repository secret
4. Name: `DOCKER_PAT`, Value: *(your token)*

### Trigger a Build

- Push to `main` branch, or
- Go to Actions → "Build and Push Custom Frappe Image" → Run workflow

The image will be pushed to `hisham733/erpnext-custom:v16`.

## Deploy

```bash
docker compose -f shrdc-compose.yml up -d
```

Wait a few minutes for the site to be created. Check progress:

```bash
docker compose -f shrdc-compose.yml logs create-site -f
```

Once complete, access ERPNext at http://localhost:8080

- **Username**: Administrator
- **Password**: admin

## Update Deployment

To update an existing deployment with a new image without data loss:

```bash
cd shrdc-erpnext
docker compose -f shrdc-compose.yml pull
docker compose -f shrdc-compose.yml up -d
```

All data is preserved. To sync workspace/fixture changes:

```bash
docker compose -f shrdc-compose.yml exec backend bench --site frontend migrate
```

## Backup

```bash
docker compose -f shrdc-compose.yml exec backend bench --site frontend backup
```

## Customize

Edit `apps.json` to add or remove apps, then push to trigger a new build.
