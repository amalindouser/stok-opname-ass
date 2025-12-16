# Panduan Penggunaan Stock Opname di Mobile

## Alur Kerja untuk HP/Tablet

### 1. **Input Data SO**
   - Buka website: https://catat-so.vercel.app
   - Isi Nama Area (gudang/warehouse)
   - Input kode barang + stok real
   - Nama otomatis muncul
   - Klik "Tambah"

### 2. **Export & Kirim ke WhatsApp**

   **Klik tombol "📥 Export & Kirim WA":**
   
   ✅ **Otomatis terjadi:**
   1. File Excel didownload ke **Downloads folder**
   2. WhatsApp dibuka otomatis
   3. Pesan siap dengan summary data
   
   ✅ **Yang harus Anda lakukan:**
   1. Di WhatsApp, **attach file** dari Downloads
   2. Cari file dengan nama: `{nama_area}_SO.xlsx`
   3. Klik send

### 3. **Contoh Flow**

   ```
   1. Isi form:
      - Nama Area: "Gudang Utama"
      - Kode: BRG001
      - Stok: 50
      
   2. Klik Tambah (repeat untuk barang lain)
   
   3. Setelah selesai, klik "📥 Export & Kirim WA"
   
   4. Terjadi:
      ✓ Gudang_Utama_SO.xlsx didownload
      ✓ WhatsApp dibuka
      ✓ Pesan otomatis + nomor penerima ready
      
   5. Anda tinggal:
      📎 Attach file dari Downloads
      ✉️ Kirim
   ```

## Detail Alur Teknis

### File Excel
- **Nama**: `{nama_area}_SO.xlsx`
- **Contoh**: `Gudang_Utama_SO.xlsx`, `Viki_SO.xlsx`
- **Lokasi Download**: `/Downloads` di HP
- **Isi**:
  - Nama Area
  - Tanggal/Jam
  - Tabel: Kode, Nama Barang, Stok Real
  - Summary total item & stok

### WhatsApp Integration
- **Nomor Tujuan**: +62 851-1731-0261 (bisa diubah)
- **Pesan Otomatis**: 
  ```
  📦 Stock Opname - {Area}
  
  📋 Data SO sudah ready
  
  File: {nama_file}
  Tanggal: DD/MM/YYYY HH:MM
  Total Item: X
  Total Stok: Y
  ```

- **Penerima wajib attach file** (sistem belum bisa auto-send file)
- Tekan Send

## Troubleshooting

### Q: File tidak bisa didownload
- Izin download mungkin ditolak browser
- Coba: Buka Settings → Privacy → Allow downloads
- Atau gunakan browser berbeda

### Q: WhatsApp tidak terbuka
- Pastikan WhatsApp sudah terinstall
- Di Android: Sistem akan auto-detect app
- Di iOS: Mungkin butuh manual open WhatsApp

### Q: File tidak ketemu di Downloads
- Cek folder: Settings → Files/Downloads
- Nama file: `{nama_area}_SO.xlsx`
- Jika tidak ada, cek browser history/downloads

### Q: Ingin attach file dari cloud
- Upload file ke Google Drive
- Share link di WhatsApp
- (Untuk versi advanced)

## Tips Penggunaan

1. **Gunakan nama area yang singkat** → Nama file lebih pendek
   - ✅ "Gudang A"
   - ❌ "Gudang Penyimpanan Barang Elektronik Utama"

2. **Cek data sebelum submit** → Dialog konfirmasi otomatis

3. **Download file tepat sebelum kirim** → Jangan close browser dulu

4. **Offline mode** → Bisa input data tanpa koneksi, tapi export butuh internet

## Alternatif (jika WhatsApp tidak bisa attach file)

### Opsi 1: Email
- Buka email di HP
- Attach file dari Downloads
- Kirim ke: admin@example.com

### Opsi 2: Cloud Drive
- Upload file ke Google Drive
- Share folder dengan penerima
- Send link via WhatsApp

### Opsi 3: Telegram Bot
- Bot bisa menerima file otomatis
- (Butuh setup bot terlebih dahulu)

---

**Versi**: 1.0
**Terakhir Update**: Desember 2025
