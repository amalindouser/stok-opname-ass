# Firebase Setup untuk Stock Opname

## Step 1: Create Firebase Project
1. Buka https://console.firebase.google.com
2. Klik **"Create Project"**
3. Nama: `stok-opname`
4. Skip Google Analytics (optional)
5. Create

## Step 2: Setup Firebase Storage
1. Di sidebar → **Storage**
2. Klik **"Create Bucket"**
3. Lokasi: `asia-southeast1` (Indonesia terdekat)
4. Pilih **"Start in test mode"** (untuk development)
5. Create

## Step 3: Setup Service Account
1. **Project Settings** (gear icon) → **Service Accounts**
2. Klik **"Generate new private key"**
3. Download JSON file (simpan sebagai `firebase-key.json`)
4. **Jangan di-commit ke GitHub** (masuk .gitignore)

## Step 4: Tambah ke Project
1. Simpan `firebase-key.json` di root folder project
2. Jangan push ke GitHub (sudah di .gitignore)
3. Berikan file ini ke VCS/deploy hanya saat production

## Step 5: Set Firebase Rules (Development)
Di **Storage** → **Rules**, ganti dengan:

```
rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    match /so/{filename} {
      // Allow read untuk semua (file public)
      allow read;
      // Allow write hanya dari backend (authenticated)
      allow write: if request.auth != null;
    }
  }
}
```

Publish rules.

## Step 6: Environment Variables (Vercel)
Jika deploy ke Vercel:
1. Buka **Vercel Dashboard** → Project → **Settings** → **Environment Variables**
2. Copy isi `firebase-key.json`
3. Tambah variable: `FIREBASE_KEY` (paste JSON content)

## Firebase Free Tier Limits
- 5GB storage
- 1GB download per hari
- Cukup untuk jutaan SO records

## Next Steps
1. ✅ Create Firebase project
2. ✅ Setup Storage
3. ✅ Download service account
4. ⏳ Update app.py
5. ⏳ Test upload
6. ⏳ Deploy ke Vercel
