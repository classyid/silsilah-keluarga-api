# 🌳 Silsilah Keluarga - Aplikasi Manajemen Pohon Keluarga

## Deskripsi Proyek
Silsilah Keluarga adalah solusi komprehensif untuk mendokumentasikan, mengelola, dan menelusuri sejarah keluarga secara digital. Aplikasi ini memungkinkan pengguna untuk dengan mudah mencatat, memperbarui, dan menjelajahi informasi anggota keluarga lintas generasi.

## Fitur Utama
- 🔍 Pencarian anggota keluarga
- 🌿 Visualisasi pohon silsilah
- ➕ Tambah, edit, dan hapus anggota keluarga
- 📸 Unggah foto anggota keluarga
- 📊 Statistik keluarga
- 💾 Ekspor dan impor data
- 🔒 Manajemen database

## Teknologi yang Digunakan
- Backend: PHP
- Database: MySQL/MariaDB
- Format Pertukaran Data: JSON, CSV
- Arsitektur: RESTful API

## Dokumentasi API
Proyek ini menyediakan sejumlah endpoint API untuk interaksi dengan data keluarga:
1. Pencarian Anggota
2. Pohon Silsilah
3. Detail Anggota
4. Statistik Keluarga
5. Manajemen Anggota (Tambah/Update/Hapus)
6. Unggah Foto
7. Ekspor/Impor Data
8. Backup Database

## Persyaratan Sistem
- PHP 7.4+
- MySQL 5.7+
- Dukungan ekstensi JSON
- Ruang penyimpanan untuk foto dan backup

## Instalasi
1. Clone repository
2. Konfigurasi database
3. Impor skema database
4. Sesuaikan file konfigurasi
5. Jalankan menggunakan web server (Apache/Nginx)

# 🔧 Dokumentasi Teknis API Silsilah Keluarga

## Pendahuluan
Dokumen ini berisi spesifikasi teknis lengkap untuk API Silsilah Keluarga, yang memungkinkan manajemen komprehensif data anggota keluarga.

## 🌐 Endpoint Utama
Base URL: `https://familytree.classy.id/`

## 📡 Daftar API Endpoints

### 1. Pencarian Anggota (`public_search.php`)
- **Metode**: GET
- **Deskripsi**: Mencari anggota keluarga berdasarkan kata kunci
- **Parameter**:
  - `q` (wajib): Kata kunci pencarian
  - `limit` (opsional): Batasan jumlah hasil (default: 10, maks: 50)
  - `generation` (opsional): Filter berdasarkan generasi

#### Contoh Request
```
GET /public_search.php?q=%25&limit=100
```

#### Contoh Respons Sukses
```json
{
  "success": true,
  "message": "Pencarian berhasil",
  "count": 13,
  "data": [
    {
      "id": 5,
      "name": "Agus Suroso",
      "generation": 1,
      "generation_label": "Anak",
      "status": "Hidup",
      "spouse": "Tin",
      "spouse_status": "Hidup"
    }
  ]
}
```

### 2. Pohon Silsilah (`public_tree.php`)
- **Metode**: GET
- **Deskripsi**: Mendapatkan struktur pohon silsilah keluarga
- **Parameter**:
  - `id` (opsional): ID anggota sebagai root pohon
  - `depth` (opsional): Kedalaman pohon (default: 3, maks: 5)

#### Contoh Request
```
GET /public_tree.php?id=1&depth=3
```

### 3. Detail Anggota (`public_member.php`)
- **Metode**: GET
- **Deskripsi**: Mendapatkan informasi detail seorang anggota
- **Parameter**:
  - `id` (wajib): ID anggota keluarga

#### Contoh Request
```
GET /public_member.php?id=1
```

### 4. Statistik Keluarga (`public_statistics.php`)
- **Metode**: GET
- **Deskripsi**: Mendapatkan statistik keseluruhan silsilah keluarga

### 5. Tambah Anggota (`add_member.php`)
- **Metode**: POST
- **Deskripsi**: Menambahkan anggota keluarga baru
- **Parameter Form Data**:
  - `name` (wajib): Nama anggota
  - `generation` (wajib): Nomor generasi
  - `parent_id` (opsional): ID orang tua
  - `deceased` (opsional): Status hidup/meninggal
  - `spouse_name` (opsional): Nama pasangan
  - Dan lain-lain...

#### Contoh Request
```
POST /add_member.php
Content-Type: application/x-www-form-urlencoded

name=Nama%20Baru&generation=2&parent_id=1&deceased=0
```

### 6. Update Anggota (`update_member.php`)
- **Metode**: POST
- **Deskripsi**: Memperbarui data anggota keluarga
- **Parameter Form Data**:
  - `id` (wajib): ID anggota yang diupdate
  - `name` (wajib): Nama anggota
  - `generation` (wajib): Nomor generasi
  - Dan parameter lainnya seperti pada tambah anggota

### 7. Hapus Anggota (`delete_member.php`)
- **Metode**: POST
- **Deskripsi**: Menghapus anggota keluarga
- **Parameter Form Data**:
  - `id` (wajib): ID anggota yang dihapus

### 8. Upload Foto (`upload_photo.php`)
- **Metode**: POST
- **Deskripsi**: Mengunggah foto anggota keluarga
- **Parameter Multipart Form Data**:
  - `member_id` (wajib): ID anggota
  - `photo` (wajib): File foto (JPG, JPEG, PNG, GIF)

### 9. Ekspor Data (`export_data.php`)
- **Metode**: POST
- **Deskripsi**: Mengekspor data silsilah keluarga
- **Parameter Form Data**:
  - `format` (wajib): Format ekspor ("json" atau "csv")

### 10. Impor Data (`import_data.php`)
- **Metode**: POST
- **Deskripsi**: Mengimpor data silsilah keluarga
- **Parameter Multipart Form Data**:
  - `import_file` (wajib): File impor (JSON atau CSV)
  - `overwrite` (opsional): Flag untuk menimpa data

### 11. Backup Database (`backup_database.php`)
- **Metode**: POST
- **Deskripsi**: Membuat backup database silsilah keluarga

## 🔒 Validasi & Keamanan
- Semua input divalidasi
- Pencegahan injeksi SQL
- Pembatasan akses
- Validasi tipe dan format data

## 🎛️ Kode Respons HTTP
- `200`: Berhasil
- `400`: Parameter tidak valid
- `404`: Sumber daya tidak ditemukan
- `405`: Metode HTTP tidak diizinkan
- `500`: Kesalahan server

## 📋 Catatan Penting
- Semua respons dalam format JSON
- Gunakan URL encoding untuk parameter
- Perhatikan batas dan validasi parameter
- Simpan token/autentikasi jika diperlukan

## 🛠️ Persyaratan Teknis
- Dukung PHP 7.4+
- Ekstensi JSON aktif
- Koneksi database yang aman
- Ruang penyimpanan mencukupi untuk foto/backup

## 🔍 Troubleshooting
- Periksa format request
- Validasi parameter input
- Periksa koneksi database
- Cek izin file dan direktori

## 📦 Versi
- Versi Dokumentasi: 1.0.0
- Terakhir Diperbarui: 27 Maret 2025

## 📞 Kontak & Support
[Informasi Kontak Tim Pengembang]
