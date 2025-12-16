# Deploy ke Vercel

## Cara Deploy

### 1. Push ke GitHub
```bash
git add .
git commit -m "Initial commit - Stock Opname App"
git push origin main
```

### 2. Buat akun Vercel
- Buka https://vercel.com
- Sign up dengan GitHub

### 3. Import Project
1. Go to https://vercel.com/dashboard
2. Click "Add New" → "Project"
3. Select repository "catat_so"
4. Click "Import"

### 4. Configure Environment (opsional)
- Framework: Python (auto-detected)
- Root Directory: ./
- Environment Variables: None needed

### 5. Deploy
- Click "Deploy"
- Tunggu proses deploy selesai (±2-3 menit)

### 6. Test
- Klik "Visit" atau lihat URL di dashboard
- Format: https://nama-project.vercel.app

## Important Notes

### Data Folder
- File `TB_BARANG.xlsx` harus ada di `data/` folder
- Excel hasil SO disimpan temporary di memory
- Vercel tidak memiliki persistent storage (file akan hilang setelah request selesai)

**Solusi jika butuh simpan:**
- Download langsung ke device (sudah implemented)
- Atau pakai Cloud Storage (AWS S3, Google Cloud Storage)

### WhatsApp Integration
- Nomor WA di-hardcode ke +62 851-1731-0261
- Bisa di-customize di `templates/index.html`

### File Size
- Max upload: 16 MB (sudah set di app.py)

## Troubleshooting

### Error: Module not found
- Pastikan `requirements.txt` di root directory
- Vercel auto-detect Python dan install dependencies

### Port error
- Vercel auto-assign port
- App.py sudah support env variable PORT

### Data tidak tersimpan
- Normal! Vercel adalah stateless (serverless)
- User HARUS download Excel sebelum close browser

## Hubungi Support Vercel
https://vercel.com/support

---

**URL Setelah Deploy:** https://catat-so.vercel.app (atau nama yang Anda pilih)
