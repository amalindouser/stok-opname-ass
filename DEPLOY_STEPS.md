# Deploy ke Vercel via GitHub

## Step 1: Push ke GitHub

```bash
# Initialize git (jika belum)
git init

# Add all files
git add .

# Commit
git commit -m "Initial commit: Stock Opname App"

# Add remote (ganti YOUR_USERNAME dan YOUR_REPO)
git remote add origin https://github.com/YOUR_USERNAME/stok-opname.git

# Push ke GitHub
git branch -M main
git push -u origin main
```

## Step 2: Connect Vercel ke GitHub

1. Buka https://vercel.com/dashboard
2. Klik **"Add New..."** → **"Project"**
3. Pilih **"Import Git Repository"**
4. Authorize GitHub & pilih repository `stok-opname`
5. Vercel akan auto-detect Framework (Flask)
6. Configure:
   - **Root Directory**: `.` (default)
   - **Build Command**: (kosong, gunakan default)
   - **Output Directory**: (kosong)
7. Klik **"Deploy"**

## Step 3: Auto-Deploy Setup
Setelah first deploy:
- Setiap push ke `main` branch → auto-deploy ke production
- Setiap PR → auto-deploy ke preview URL

## Step 4: Environment Variables (Penting!)
Jika pakai PostgreSQL (recommended):

1. Di Vercel Dashboard → Project Settings → **Environment Variables**
2. Add:
   - `POSTGRES_URL` (dari Vercel Postgres atau Supabase)
   - `FLASK_ENV=production`
3. Redeploy

## Current Issue: Database
⚠️ **SQLite database akan hilang** setiap deploy (Vercel ephemeral filesystem).

### Solution:
Migrate ke PostgreSQL (lihat `DATABASE_MIGRATION.md`)

### Untuk sekarang (development only):
App akan berjalan tapi data reset setiap deploy.

## Step 5: Update Requirements.txt (jika pakai PostgreSQL)
```
Flask==2.3.0
openpyxl==3.10.0
psycopg2-binary==2.9.9
```

## Commands Reference

```bash
# Local development
python app.py

# Deploy baru
git push origin main

# Check logs di Vercel
# → Vercel Dashboard → Deployments → View Logs

# Rollback
# → Vercel Dashboard → Deployments → Promote to Production
```

## Troubleshooting

### Error: "Read-only file system"
→ Vercel FS read-only, gunakan `/tmp` atau database cloud

### Database data hilang
→ SQLite tidak persistent di Vercel, pakai PostgreSQL

### 502 Bad Gateway
→ Cek logs di Vercel dashboard

## Next Steps

1. ✅ Create GitHub repository
2. ✅ Push code
3. ✅ Connect ke Vercel
4. ⏳ Migrate ke PostgreSQL (untuk production)
