# Stock Opname Web App

Aplikasi web sederhana untuk input data Stock Opname TANPA database.

## Struktur Folder

```
catat_so/
├── app.py                 # Backend Flask
├── requirements.txt       # Dependencies
├── README.md             # Dokumentasi
├── templates/
│   └── index.html        # Frontend HTML/CSS/JS
├── data/
│   └── TB_BARANG.xlsx    # Master barang (input file Anda)
└── __pycache__/          # Cache Python (auto-generated)
```

## Setup & Instalasi

### 1. Clone/Download Proyek
```bash
cd catat_so
```

### 2. Install Dependencies
```bash
pip install -r requirements.txt
```

### 3. Siapkan Master Barang
- Letakkan file `TB_BARANG.xlsx` di folder `data/`
- Format file harus:
  - Sheet pertama berisi data
  - Harus ada kolom **KODE** dan **NAMA**
  - Data mulai dari baris ke-2 (baris 1 adalah header)
  - Kolom lain (KATEGORI, DEPARTEMEN, STOK, dll) akan diabaikan

### 4. Jalankan Aplikasi
```bash
python app.py
```

Output:
```
 * Running on http://127.0.0.1:5000
```

### 5. Akses di Browser
Buka browser dan akses: **http://127.0.0.1:5000**

## Fitur Utama

### 1. Input Data SO
- User hanya boleh mengisi **Kode Barang** dan **Stok Real**
- **Nama Barang** otomatis muncul dari master barang (TB_BARANG.xlsx)
- Validasi kode barang saat input blur

### 2. Validasi
- Kode barang harus ada di master
- Stok real harus berupa angka
- Tidak boleh ada duplikat kode barang

### 3. Manajemen Data
- Tambah data baru
- Hapus data individual
- Reset semua data
- View statistik (total item, total stok)

### 4. Auto Fill
- Dropdown untuk memilih dari master barang
- Kode dan nama otomatis terisi

### 5. Export
- Download hasil SO ke file Excel (`hasil_so_YYYYMMDD_HHMMSS.xlsx`)

## API Endpoints

### GET /
Menampilkan halaman utama web interface.

### GET /api/master-barang
Mengembalikan semua data master barang dalam format JSON.

**Response:**
```json
{
  "BRG001": "Kipas Angin",
  "BRG002": "Lampu LED 10W"
}
```

### POST /api/validasi-kode
Validasi kode barang.

**Request:**
```json
{
  "kode": "BRG001"
}
```

**Response (valid):**
```json
{
  "valid": true,
  "nama_barang": "Kipas Angin"
}
```

**Response (invalid):**
```json
{
  "valid": false,
  "message": "Kode BRG999 tidak ditemukan di master barang"
}
```

### POST /api/tambah-so
Menambah data SO baru.

**Request:**
```json
{
  "kode_barang": "BRG001",
  "nama_barang": "Kipas Angin",
  "stok_real": 25
}
```

**Response:**
```json
{
  "success": true,
  "data": [...]
}
```

### GET /api/daftar-so
Mengembalikan semua data SO yang sudah diinput.

**Response:**
```json
[
  {
    "kode_barang": "BRG001",
    "nama_barang": "Kipas Angin",
    "stok_real": 25
  }
]
```

### DELETE /api/hapus-so/<index>
Menghapus data SO berdasarkan index.

### POST /api/reset-so
Menghapus semua data SO.

### POST /api/export-excel
Download hasil SO ke Excel.

## Catatan Penting

1. **In-Memory Storage**: Data SO disimpan di memory. Jika aplikasi di-restart, semua data hilang.
   - Solusi: User harus export Excel sebelum aplikasi ditutup.

2. **Master Barang**: Hanya bisa baca dari file. Untuk edit master, gunakan Excel langsung.

3. **Single User**: Aplikasi ini sederhana untuk internal saja, tidak ada fitur multi-user.

4. **Port**: Default port 5000. Jika sudah terpakai, ubah di `app.py` baris terakhir.

## Troubleshooting

### Error: "TB_BARANG.xlsx tidak ditemukan"
- Pastikan file berada di folder `data/`
- Folder `data/` harus sudah ada di root proyek

### Error: Port 5000 sudah digunakan
Ubah port di `app.py`:
```python
app.run(debug=True, host='127.0.0.1', port=5001)  # Ganti 5001
```

### Error: Module Flask tidak ditemukan
```bash
pip install -r requirements.txt
```

## Mengubah Struktur

### Menambah Kolom Baru
Edit `templates/index.html` dan `app.py`:
1. Tambah input field di HTML
2. Tambah field di POST request body
3. Tambah kolom di Excel export

### Mengubah Styling
Edit bagian `<style>` di `templates/index.html`

### Mengubah Port atau Host
Edit di `app.py` baris terakhir:
```python
app.run(debug=True, host='0.0.0.0', port=8000)  # Akses dari device lain
```

## Deployment

### ⭐ Vercel (Recommended)

**Langkah cepat:**

1. Push ke GitHub:
```bash
git add .
git commit -m "Stock Opname App"
git push origin main
```

2. Deploy ke Vercel:
   - Buka https://vercel.com/dashboard
   - Import project dari GitHub
   - Click Deploy
   - Done! URL: `https://catat-so.vercel.app`

**Detail:** Lihat `DEPLOY_VERCEL.md`

---

### Opsi lain:

#### Railway
1. Go to https://railway.app
2. New Project → GitHub
3. Select repository → Auto-deploy

#### Heroku
```bash
heroku login
heroku create nama-app-anda
git push heroku main
```

#### Docker (Local)
```bash
docker-compose up
# Akses: http://localhost:5000
```

#### Production Gunicorn
```bash
gunicorn -w 4 -b 0.0.0.0:5000 wsgi:app
```

## Troubleshooting Deployment

**Error: pyodbc not found**
- Pastikan tidak ada import pyodbc di kode
- requirements.txt hanya berisi: Flask, Werkzeug, openpyxl

**File Excel tidak tersimpan di cloud**
- Gunakan persistent storage (Heroku Dyno, Railway volume, dll)
- Atau simpan ke cloud storage (AWS S3, Google Cloud Storage)

**Port conflict**
- Edit PORT di app.py atau set env variable PORT=8000

## License

Free untuk penggunaan internal.
