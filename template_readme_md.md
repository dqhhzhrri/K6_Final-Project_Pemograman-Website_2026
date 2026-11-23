# [Nama Aplikasi Web Anda]

Deskripsi singkat mengenai aplikasi web yang dibangun (contoh: Aplikasi Sistem Informasi Peminjaman Alat Laboratorium berbasis web untuk mengelola inventaris dan proses pengajuan peminjaman secara terintegrasi).

**Mata Kuliah:** Pemrograman Web (ET234305) - Semester 3  
**Departemen:** Teknologi Informasi, Institut Teknologi Sepuluh Nopember (ITS)  
**Kelompok:** [Nomor/Nama Kelompok]

---

## 👥 Anggota Kelompok & Kontribusi

| No | Nama Lengkap | NRP | GitHub | Peran / Kontribusi Utama |
| :--- | :--- | :--- | :--- | :--- |
| 1 | George David Nebore | 5027221043 | [@daveyurbae](https://github.com/daveyurbae) | [Contoh: Perancangan Database, ERD, & Backend API] |
| 2 | Mey Rosalina | 5027241004 | [@meyrosa](https://github.com/meyrosa) | [Contoh: Implementasi Aturan Bisnis, Transaksi DB, & Auth] |
| 3 | Farrel Arteya Kumara | 5027251020 | [@FarrelKumara15](https://github.com/FarrelKumara15) | [Contoh: Frontend React (Halaman Daftar, Detail, & Form)] |
| 4 | Sean Arthur Tamajaya | 5027251050 | [@minecraftsean321-ops](https://github.com/minecraftsean321-ops) | [Contoh: Frontend Dashboard Monitoring & Styling] |
| 5 | D'Qhaizhar Ari Dhiaulhaq | 5027251083 | [@dqhhzhrri](https://github.com/dqhhzhrri) | [Contoh: Integrasi API, Pengujian (QA), & Dokumentasi] |

---

## 📋 Analisis Singkat Proses Bisnis

### 1. Pengguna Aplikasi & Masalah yang Diselesaikan
* **Aktor / Pengguna:**
  * **[Role 1, misal: Peminjam/Mahasiswa]:** [Jelaskan kebutuhan dan masalah yang dihadapi].
  * **[Role 2, misal: Admin/Laboran]:** [Jelaskan kebutuhan dan masalah yang dihadapi].
* **Solusi & Hasil yang Dicapai:** [Jelaskan bagaimana aplikasi ini menyelesaikan masalah dari awal hingga akhir dalam satu alur terintegrasi].

### 2. Status, Percabangan Keputusan, & Tindakan yang Diizinkan
Aplikasi ini memiliki **[Jumlah, min. 4]** status utama dalam siklus proses bisnisnya:
1. **[Status 1, misal: Diajukan]:** [Jelaskan kondisi status dan tindakan apa saja yang diizinkan pada status ini].
2. **[Status 2, misal: Disetujui]:** [Jelaskan percabangan keputusan dan tindakan yang diizinkan].
3. **[Status 3, misal: Ditolak]:** [Jelaskan kondisi status akhir ini].
4. **[Status 4, misal: Dikembalikan]:** [Jelaskan kondisi status dan perubahan data yang terjadi].

### 3. Aturan Bisnis & Transaksi Basis Data (Backend)
* **Pembatasan Perpindahan Status:** [Contoh: Pengajuan berstatus *Ditolak* atau *Dikembalikan* tidak dapat diubah kembali menjadi *Disetujui*].
* **Pemeriksaan Batas Data Tersimpan:** [Contoh: Sistem memvalidasi apakah stok alat mencukupi sebelum menyetujui peminjaman].
* **Pencegahan Tindakan Ganda/Bertentangan:** [Contoh: Mencegah persetujuan ganda pada pengajuan yang sudah berstatus *Disetujui*].
* **Database Transaction (Prisma `$transaction`):** [Jelaskan aksi yang menggunakan transaksi atomik, misal: Saat penyetujuan peminjaman, sistem mengubah status peminjaman, mengurangi stok pada tabel Alat, dan mencatat riwayat ke tabel Log secara bersamaan. Jika salah satu gagal, seluruh perubahan dibatalkan (*rollback*)].

---

## 🗄️ Perancangan Database (ERD)

Database menggunakan **PostgreSQL** dengan ORM **Prisma**, terdiri dari minimal 4 tabel dengan relasi induk–detail serta relasi *many-to-many* melalui tabel penghubung.

* **Daftar Tabel:**
  1. `[Nama_Tabel_1]` (Induk)
  2. `[Nama_Tabel_2]` (Master/Kategori)
  3. `[Nama_Tabel_3]` (Detail / Penghubung Many-to-Many)
  4. `[Nama_Tabel_4]` (Log Aktivitas / Pengguna)

> **Catatan:** Letakkan gambar diagram ERD Anda di folder proyek (misal: `docs/erd.png`) dan sesuaikan tautan di bawah ini.

![Entity Relationship Diagram](docs/erd.png)

---

## 🚀 Cara Menjalankan Aplikasi (Localhost)

### Prasyarat
* Node.js (v18 atau terbaru)
* PostgreSQL (Lokal atau Neon DB)
* Git

### 1. Clone Repositori
```bash
git clone [URL_REPOSITORI_ANDA]
cd [NAMA_FOLDER_PROYEK]
```

### 2. Konfigurasi & Menjalankan Backend (Express + Prisma)
```bash
cd backend
npm install

# Salin file environment dan sesuaikan DATABASE_URL PostgreSQL Anda
cp .env.example .env

# Jalankan migrasi database dan data awal (seed)
npx prisma migrate dev
npx prisma db seed

# Jalankan server backend
npm run dev
```
*Server backend akan berjalan di `http://localhost:[PORT_BACKEND]`.*

### 3. Konfigurasi & Menjalankan Frontend (React + Tailwind CSS)
Buka terminal baru, lalu jalankan perintah berikut:
```bash
cd frontend
npm install

# Salin file environment jika diperlukan (misal: VITE_API_URL)
cp .env.example .env

# Jalankan aplikasi frontend
npm run dev
```
*Aplikasi frontend dapat diakses melalui browser di `http://localhost:[PORT_FRONTEND]`.*

---

## 🧪 Bukti Skenario Pengujian

Berikut adalah bukti pengujian yang mencakup alur berhasil (*positive case*), penanganan kesalahan (*negative case*), dan kesesuaian data dashboard.

### 1. Skenario Alur Berhasil (*Positive Case*)
* **Deskripsi Uji:** [Contoh: Pengguna mengajukan peminjaman 2 Kabel HDMI dan 1 Proyektor, Admin menyetujui pengajuan, stok alat berkurang sesuai jumlah, status berubah menjadi *Disetujui*, hingga alat dikembalikan dan stok bertambah kembali].
* **Hasil yang Diharapkan:** Data tersimpan di database, stok terbarui secara akurat melalui transaksi, dan log tercatat.
* **Bukti Tangkapan Layar:**
  ![Bukti Positive Case](docs/test-positive.png)

### 2. Skenario Kasus Negatif (*Negative Case*)
* **Skenario A - Stok Tidak Mencukupi:**
  * **Deskripsi Uji:** [Contoh: Mencoba menyetujui pengajuan peminjaman saat stok Proyektor habis/kurang dari jumlah yang diminta].
  * **Hasil:** Sistem menolak transaksi, menampilkan pesan validasi error dari API, status tetap *Diajukan*, dan stok alat lain tidak ikut berkurang (*rollback*).
  * **Bukti Tangkapan Layar:**
    ![Bukti Negative Case Stok](docs/test-negative-stok.png)

* **Skenario B - Permintaan Berulang / Tindakan Ganda:**
  * **Deskripsi Uji:** [Contoh: Mengirim ulang permintaan persetujuan pada pengajuan yang sudah berstatus *Disetujui*].
  * **Hasil:** Sistem memblokir perubahan status dan memastikan stok tidak berkurang dua kali.
  * **Bukti Tangkapan Layar:**
    ![Bukti Negative Case Duplikat](docs/test-negative-duplicate.png)

### 3. Kesesuaian Dashboard Monitoring dengan Data
* **Deskripsi Uji:** [Contoh: Mencocokkan angka ringkasan/rekap pada halaman Dashboard berdasarkan kategori atau status dengan keseluruhan data yang memenuhi filter, termasuk data yang berada di halaman pagination berikutnya].
* **Hasil:** Angka pada kartu ringkasan dashboard otomatis terbarui dan akurat 100% dengan total data di database.
* **Bukti Tangkapan Layar:**
  ![Bukti Dashboard Monitoring](docs/test-dashboard.png)

---

## 📸 Tangkapan Layar Antarmuka Aplikasi

| Halaman Login & Autentikasi | Halaman Dashboard Monitoring |
| :---: | :---: |
| ![Login](docs/ss-login.png) | ![Dashboard](docs/ss-dashboard.png) |

| Halaman Daftar (Filter, Search, Pagination) | Halaman Detail & Formulir Aksi |
| :---: | :---: |
| ![Daftar](docs/ss-list.png) | ![Detail](docs/ss-detail.png) |
