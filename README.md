# SI PATUH (Sistem Informasi Penjadwalan Pengawasan Tahunan Terpadu dan Humanis)
### Inspektorat Daerah Pemerintah Kabupaten Probolinggo

SI PATUH adalah aplikasi web *enterprise* internal resmi untuk mengelola Program Kerja Pengawasan Tahunan (PKPT), jadwal audit lapangan, monitoring progres realisasi, kelengkapan dokumen pengawasan, serta pelaporan multi-tahun di lingkungan Inspektorat Kabupaten Probolinggo.

---

## 🏛️ Arsitektur & Teknologi

1. **Frontend**: React 19 + TypeScript + Vite.
2. **Styling & Desain**: Tailwind CSS (Enterprise Government Palette: Navy Utama `#142B4A`, Navy Gelap `#0B1B30`, Gold Aksen `#C6A15B`, Background `#F4F6F9`, Inter Font).
3. **Icons**: Lucide Icons.
4. **Database Utama**: PostgreSQL melalui Supabase (dengan skrip SQL Migration & Row Level Security / RLS).
5. **Autentikasi**: Supabase Auth terintegrasi Role-Based Access Control (RBAC).
6. **File & Dokumen**: Supabase Storage + Integrasi Folder Google Drive (Kolom 20 G-DRIVE).
7. **Penyimpanan Lokal & Offline Resilience**: Sinkronisasi data otomatis dengan penyimpanan lokal sehingga aplikasi langsung dapat digunakan tanpa ketergantungan wajib.
8. **Export & Import**: Microsoft Excel (.xlsx) dengan SheetJS & PDF Resmi Berkop Surat dengan jsPDF-AutoTable.

---

## 📋 Struktur Resmi 20 Kolom "KEGIATAN BIDANG"

Sesuai ketentuan, tabel teknis `kegiatan_bidang` mempertahankan seluruh 20 kolom asli tanpa perubahan nama kolom maupun urutannya:

| No. | Nama Kolom Resmi | Tipe Data & Keterangan |
|---|---|---|
| 1 | **NO** | Nomor urut baris tampilan |
| 2 | **ID** | Kode unik bisnis, contoh: `2026-PKPT-001`, `2027-PKPT-001` |
| 3 | **TANGGAL** | Tanggal target batas akhir pengawasan |
| 4 | **BULAN** | Bulan pelaksanaan (Januari - Desember) |
| 5 | **BIDANG** | KUAS, PEMAPAR, SOSBUD, PEREKONOMIAN, INVESTIGASI |
| 6 | **KEGIATAN** | Nama lengkap kegiatan pengawasan (Wajib) |
| 7 | **SASARAN** | OPD, Puskesmas, BLUD, atau Desa obyek pengawasan |
| 8 | **SUB GIAT** | Rincian uji petik fisik atau administrasi |
| 9 | **HARI TERSISA** | Dihitung otomatis oleh sistem berdasarkan tanggal hari ini |
| 10 | **STATUS PELAKSANAAN KEGIATAN** | Belum Dilaksanakan, Mulai, Proses, Selesai, Ditunda, Batal |
| 11 | **ANGGARAN** | Pagu anggaran kegiatan (Format Rupiah) |
| 12 | **REALISASI (USER)** | Realisasi belanja pengawasan (Format Rupiah) |
| 13 | **LAPORAN HASIL** | Nomor LHP atau status penerbitan laporan |
| 14 | **RTL** | Status Rencana Tindak Lanjut rekomendasi LHP |
| 15 | **SPJ** | Kelengkapan Surat Pertanggungjawaban |
| 16 | **KESESUAIAN PKPT** | Sesuai, Tidak Sesuai, Penyesuaian, Tambahan |
| 17 | **KETERANGAN** | Catatan teknis pengawasan |
| 18 | **TANGGAL MULAI PENGAWASAN** | Tanggal surat tugas / entry meeting |
| 19 | **KETEPATAN WAKTU** | Tepat Waktu, Terlambat, Sedang Berjalan, Belum Dimulai |
| 20 | **G-DRIVE** | Tautan folder / berkas Google Drive Inspektorat |

---

## 🎨 Identitas 5 Bidang Inspektorat Kabupaten Probolinggo

| Bidang | Warna Identitas | Nama Irban |
|---|---|---|
| **KUAS** | Kuning (`#EAB308`) | Irban Wilayah I (Keuangan & Aset) |
| **PEMAPAR** | Hijau (`#16A34A`) | Irban Wilayah II (Pemerintahan & Aparatur) |
| **SOSBUD** | Abu-abu (`#64748B`) | Irban Wilayah III (Sosial Budaya) |
| **PEREKONOMIAN** | Merah Muda (`#EC4899`) | Irban Wilayah IV (Perekonomian & BUMD) |
| **INVESTIGASI** | Biru (`#2563EB`) | Irban Khusus (Investigasi & Dumas) |

---

## 👥 5 Peran Pengguna (Role-Based Access Control / RBAC)

1. **Administrator**: Pengelolaan seluruh aplikasi, hak akses pengguna, tahun anggaran, duplikasi template PKPT, dan audit log.
2. **Inspektur**: Akses eksekutif ke seluruh dashboard, pemantauan seluruh bidang, disposisi, dan laporan resmi.
3. **Sekretariat**: Mengelola kelengkapan administrasi pengawasan, rekapitulasi, dan dokumen SPJ.
4. **Irban/Kepala Bidang**: Mengelola kegiatan dan memantau progres pelaksanaan bidang masing-masing.
5. **Auditor/PPUPD**: Pelaksanaan penugasan audit lapangan, pembaruan status progres, dan unggah dokumen kerja.

---

## 🚀 Panduan Menjalankan Secara Lokal (Visual Studio Code)

Aplikasi ini dapat diunduh (ZIP), dikembangkan di VS Code, dan disinkronkan ke GitHub:

```bash
# 1. Clone repository atau ekstrak ZIP
git clone <repo_url>
cd sipatuh-probolinggo

# 2. Pasang dependencies
npm install

# 3. Buat file .env dari template
cp .env.example .env

# 4. (Opsional) Masukkan kredensial Supabase Anda di .env:
# VITE_SUPABASE_URL=https://your-project.supabase.co
# VITE_SUPABASE_ANON_KEY=your-anon-key

# 5. Jalankan aplikasi di lingkungan lokal
npm run dev
```

Server development akan berjalan di `http://localhost:3000`.

---

## 🗄️ Menjalankan Database di Supabase PostgreSQL

1. Buat proyek baru di [Supabase Console](https://supabase.com).
2. Buka menu **SQL Editor**.
3. Buka berkas `src/lib/databaseSchema.sql` pada repository ini.
4. Salin seluruh isi SQL dan jalankan (*Run*) di Supabase SQL Editor.
5. Salin *Project URL* dan *anon public key* ke menu **Pengaturan & Supabase** di aplikasi SI PATUH atau ke file `.env`.
