# Surenatech Website — Azure Static Web Apps Deployment

## Files in this package

| File | Purpose |
|------|---------|
| `index.html` | The complete Surenatech website (single-file) |
| `staticwebapp.config.json` | Azure SWA routing, headers & security config |
| `.github/workflows/azure-static-web-apps.yml` | GitHub Actions CI/CD pipeline |

---

## Quick Deploy (Azure Portal — No GitHub needed)

1. Go to [portal.azure.com](https://portal.azure.com)
2. Search for **Static Web Apps** → **+ Create**
3. Fill in:
   - **Resource Group**: Create new or select existing
   - **Name**: `surenatech-website`
   - **Plan**: Free (works perfectly for this site)
   - **Region**: Central India / Southeast Asia (closest to Hyderabad)
4. For **Deployment source**: choose **Other** (manual upload)
5. Click **Review + Create** → **Create**
6. Once created, go to the resource → **Manage deployment token** → copy the token
7. Use the [Azure SWA CLI](https://azure.github.io/static-web-apps-cli/) to deploy:

```bash
npm install -g @azure/static-web-apps-cli
swa deploy ./  --deployment-token <YOUR_TOKEN>  --env production
```

---

## Deploy via GitHub Actions (Recommended for CI/CD)

### Step 1 — Push to GitHub
```bash
git init
git add .
git commit -m "Initial Surenatech website"
git branch -M main
git remote add origin https://github.com/<your-username>/surenatech-website.git
git push -u origin main
```

### Step 2 — Create Azure Static Web App linked to GitHub
1. Go to **Azure Portal** → **Static Web Apps** → **+ Create**
2. **Deployment source**: GitHub
3. Authorize and select your repo + `main` branch
4. **App location**: `/`  |  **Output location**: `` (leave empty)
5. Azure auto-creates the GitHub Actions secret and workflow file

### Step 3 — Done!
Every push to `main` automatically deploys. PRs get a preview URL.

---

## Security headers included
The `staticwebapp.config.json` ships with:
- `X-Content-Type-Options: nosniff`
- `X-Frame-Options: SAMEORIGIN`
- `Referrer-Policy: strict-origin-when-cross-origin`
- `Content-Security-Policy` scoped to fonts.googleapis.com

---

## Custom Domain (optional)
1. In Azure Portal → your Static Web App → **Custom domains** → **+ Add**
2. Enter `www.surenatech.in` → follow CNAME instructions with your DNS registrar
3. Azure provisions a free TLS/SSL certificate automatically

---

*Built with Azure Static Web Apps · Surenatech Technologies Pvt. Ltd.*
