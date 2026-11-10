# 📋 Product Requirements Document (PRD): UNTAG Event Hub

**Nama Produk:** UNTAG Event Hub  
**Tim Pengembang:** Kelompok 9 (Pinkan Dea Sastri Yuliana, Evania Junia Amanda, La Ode Nauval Aqiilah Tsaqif)  
**Status Dokumen:** Approved for Module 7 Development  

---

## 1. Product Overview (Latar Belakang & Masalah)

### 1.1 Latar Belakang Masalah
Berdasarkan riset kualitatif (In-Depth Interview) dan survei terhadap mahasiswa aktif Universitas 17 Agustus 1945 (UNTAG) Surabaya pada Modul 1 hingga Modul 3, ditemukan 4 masalah utama dalam ekosistem informasi kegiatan kampus:
1. **Fragmentasi Informasi:** Pengumuman acara tersebar di lebih dari 15 akun Instagram Ormawa (BEM, DPM, HIMA, UKM) dan grup WhatsApp angkatan yang cepat tertimbun ratusan pesan tugas kuliah.
2. **Risiko Tinggi Terlewat Deadline:** 9 dari 10 mahasiswa mengaku pernah terlambat mendaftar acara karena fitur Save Post di Instagram atau forward chat WhatsApp tidak memiliki pengingat batas waktu pendaftaran.
3. **Ketidakpastian Poin SKPI:** Poster acara sering kali hanya mencantumkan "Free E-Sertifikat" tanpa kejelasan apakah sertifikat tersebut diakui oleh Biro Kemahasiswaan untuk klaim poin SKPI (SIMPOINT) beserta besaran bobot poinnya.
4. **Friksi Pendaftaran Berulang:** Setiap kepanitiaan menggunakan Google Form terpisah yang mewajibkan mahasiswa mengetik ulang data diri (NBI) serta mengunggah bukti screenshot share poster ke 5 grup WhatsApp dan tag 5 teman di Instagram, yang memicu tingginya angka batal daftar (drop-off).

### 1.2 Pernyataan Masalah (Point of View / POV)
> "Mahasiswa aktif UNTAG Surabaya yang mengejar poin SKPI sangat membutuhkan satu sumber informasi kegiatan kampus dan luar kampus yang lengkap dengan kejelasan status poin SKPI dan batas waktu pendaftaran, karena mereka secara diam-diam mengalami ketinggalan kegiatan dan batal mendaftar akibat informasi yang cepat tenggelam di grup WhatsApp/Instagram serta syarat pendaftaran manual yang berbelit-belit."

### 1.3 Unique Value Proposition (UVP)
Satu portal navigasi kegiatan mahasiswa UNTAG Surabaya yang memadukan transparansi verifikasi poin SKPI, penyaringan cerdas berdasarkan deadline terdekat, serta pendaftaran cepat 1 pintu berbuah E-Tiket QR tanpa syarat spamming media sosial.

---

## 2. Target Pengguna (User Persona)

1. **Persona 1 – Rania Maharani (20 Tahun, Mahasiswi S1 Semester 5 – Kuliah Sambil Bekerja):**
   * **Kebutuhan Utama:** Menemukan kegiatan berpoin SKPI yang jadwalnya pasti (tidak bentrok jam kuliah/kerja) dan 100% terverifikasi diakui kampus dalam satu kali baca tanpa harus menghubungi CP panitia satu per satu.
   * **Pain Points:** Sering menunda membaca pengumuman di grup WA saat jam kerja hingga akhirnya lewat deadline; lelah menyatukan informasi yang terpisah antara poster IG, link bio, dan grup WA.
2. **Persona 2 – Dini Angraini / Bagas Adi (20 Tahun, Mahasiswa S1 Semester 5 FTEIC – Pemburu Target SKPI):**
   * **Kebutuhan Utama:** Alur pendaftaran acara yang praktis (kurang dari 2 menit) serta kemudahan mengakses bukti tiket dan riwayat kepesertaan untuk dilaporkan ke portal SIMPOINT kampus.
   * **Pain Points:** Langsung membatalkan pendaftaran ketika melihat syarat wajib repost ke 5 grup WA dan upload screenshot satu per satu di Google Form; sering lupa pada poster yang hanya disimpan di Save Post Instagram.

---

## 3. Alur Sistem Utama (User Flow)

Alur interaksi pengguna dirancang bebas jalan buntu (Zero Dead-End Flows) dengan tahapan sebagai berikut:
1. **Autentikasi (01_Login & 02_Login_Error):** Mahasiswa masuk menggunakan 10 digit NBI dan kata sandi. Jika NBI kurang dari 10 digit, sistem menampilkan validasi galat ("⚠️ NBI harus terdiri dari 10 digit angka") dan menonaktifkan tombol masuk hingga input diperbaiki.
2. **Eksplorasi Beranda (03_Beranda):** Mahasiswa melihat Hero Banner informasi portal dan daftar 3 Kegiatan Terdekat Minggu Ini, lalu menekan tombol Jelajahi Katalog Acara.
3. **Penyaringan Katalog (04_Katalog):** Mahasiswa menyaring kegiatan menggunakan Sidebar Filter (Status Ber-SKPI, Kategori Seminar/Workshop/Lomba, Bulan Pelaksanaan, & Toggle Kuota Tersedia) serta mengurutkan berdasarkan Deadline Terdekat.
4. **Verifikasi Detail & Jadwal (05_Detail_Acara):** Mahasiswa memeriksa detail acara, lencana verifikasi poin SKPI, memilih sesi jadwal pelaksanaan, memeriksa rincian biaya (Rp 0 Gratis) serta sisa kuota, lalu mengklik Daftar Sekarang.
5. **Pengisian Formulir Bertahap (06_Form_Pendaftaran):** Mahasiswa memeriksa/mengisi data diri (Nama Lengkap, 10 digit NBI, Program Studi, Email Kampus), mencentang persetujuan kehadiran penuh, dan menekan Kirim Pendaftaran.
6. **Penerbitan E-Tiket QR (07_Sukses_Tiket):** Sistem menerbitkan kode tiket unik (#UNTAG-2026-0891) beserta Kode QR presensi yang dapat diunduh dalam format PDF.
7. **Pelacakan Riwayat (08_Riwayat_Tiket):** Mahasiswa dapat melihat kembali seluruh tiket acara pada tab Akan Datang maupun Selesai Diikuti untuk keperluan klaim sertifikat ke portal SIMPOINT.

---

## 4. Feature Breakdown (Rincian 8 Layar Figma untuk Modul 7)

Seluruh layar dirancang pada ukuran Web Desktop (1440 × 1024 px) dengan sistem 12-Column Grid (Margin: 120px, Gutter: 24px, Column Width: 78px) dan disiplin 8pt Grid System:

| Kode Layar Figma | Nama Halaman / Section | Komponen Utama yang Digunakan | Spesifikasi Fungsional untuk Koding Modul 7 |
| :--- | :--- | :--- | :--- |
| **01_Login** | Halaman Masuk Mahasiswa | • Brand Split Panel (Merah UNTAG)<br>• Input Field (Default State)<br>• Button Primer & Sekunder (Google) | Menerima input 10 digit NBI/Email dan Kata Sandi; tombol Masuk mengarahkan ke 03_Beranda. |
| **02_Login_Error** | Validasi Galat Login | • Input Field (Error State + Ikon ⚠️)<br>• Pesan Galat Eksplisit<br>• Button Primer (Disabled State) | Mempertahankan ketikan pengguna (14622001), menampilkan border merah + ikon peringatan sesuai standar WCAG SC 1.4.1, dan mengunci tombol Masuk. |
| **03_Beranda** | Beranda (Landing Page) | • Navbar Desktop (Tab Beranda Aktif)<br>• Hero Banner Card (Pola-Z)<br>• 3x Card Event Desktop | Menampilkan proposisi nilai utama portal, tombol CTA ke katalog/riwayat tiket, dan 3 kartu kegiatan terdekat dengan lencana poin SKPI & sisa waktu. |
| **04_Katalog** | Katalog & Penyaringan Acara | • Navbar Desktop (Tab Katalog Aktif)<br>• Sidebar Filter (Checkbox, Dropdown, Toggle)<br>• Category Pills & Sort Dropdown<br>• Grid 2x2 Card Event Desktop | Menyaring daftar kegiatan secara dinamis berdasarkan status SKPI, kategori, bulan, dan ketersediaan kuota, serta mengurutkan dari batas daftar (deadline) terdekat. |
| **05_Detail_Acara** | Detail Kegiatan & Jadwal | • Kartu Profil Acara (7 Kolom Grid)<br>• Badge Status (Terverifikasi SKPI)<br>• Kartu Pilih Jadwal & Rincian Pasti (5 Kolom Grid) | Menampilkan deskripsi lengkap acara, syarat peserta, radio button sesi jadwal, rincian biaya (Rp 0 Gratis), sisa kursi, dan tombol Daftar Sekarang. |
| **06_Form_Pendaftaran** | Formulir Pendaftaran (Stepper) | • Top Stepper Indicator (Langkah 1–2–3)<br>• Kartu Form 2 Kolom (780px)<br>• Input Field (Default & Focused)<br>• Checkbox Persetujuan | Menerapkan Golden Proximity Rule (jarak label ke input 8px, jarak antar baris form 24px). Memvalidasi input wajib sebelum menerbitkan tiket. |
| **07_Sukses_Tiket** | Konfirmasi Sukses & E-Tiket | • Ikon Centang Sukses Hijau<br>• Kartu E-Tiket + Gambar QR Code<br>• Button Unduh PDF & Navigasi | Menampilkan bukti pendaftaran sah, kode tiket #UNTAG-2026-0891, detail peserta, dan tombol unduh/cetak E-Tiket PDF. |
| **08_Riwayat_Tiket** | Riwayat Tiket & Kegiatan Saya | • Navbar Desktop (Tab Riwayat Aktif)<br>• Tab Switcher: Akan Datang (2) & Selesai Diikuti (3)<br>• Grid 2 Kolom Card Tiket | Menampilkan daftar acara yang telah didaftarkan mahasiswa beserta status kehadiran dan tombol akses cepat Lihat QR Tiket. |

---

## 5. Dokumentasi Design Tokens & Aksesibilitas (Standar Modul 5 ke CSS Modul 7)

Seluruh nilai warna, tipografi, dan spasi wajib dideklarasikan menggunakan CSS Custom Properties (Variables) pada tahap koding Modul 7:

### 5.1 Token Warna (Primitives & Semantics – Lulus Audit WCAG 2.2 Level AA)
| Token Semantik (Figma) | Variabel CSS (:root) | Nilai Hex | Rasio Kontras (WCAG 2.2) | Kegunaan Komponen |
| :--- | :--- | :--- | :--- | :--- |
| `surface/page` | `--surface-page` | `#F8F9FA` | — | Latar belakang utama seluruh layar aplikasi |
| `surface/card` | `--surface-card` | `#FFFFFF` | — | Latar belakang kartu, navbar, sidebar, & kolom input |
| `surface/brand-subtle` | `--surface-brand-subtle` | `#FEE8E8` | — | Latar belakang badge mendesak & pil kategori aktif |
| `text/primary` | `--text-primary` | `#1A1C1E` | **15.3 : 1** (AAA) | Teks judul utama dan isi paragraf |
| `text/secondary` | `--text-secondary` | `#44474E` | **8.4 : 1** (AAA) | Teks penyelenggara, tanggal acara, & keterangan pendukung |
| `action/primary` | `--action-primary` | `#B40000` | **7.14 : 1** (AAA) | Tombol aksi utama (Primary Button) & indikator tab aktif |
| `action/primary-hover` | `--action-primary-hover` | `#7A0000` | **10.8 : 1** (AAA) | Warna tombol utama saat di-hover atau ditekan |
| `border/default` | `--border-default` | `#E0E2EC` | — | Garis tepi kartu, navbar, dan input field normal |
| `status/verified-skpi` | `--status-verified-skpi` | `#15803D` | **5.1 : 1** (AA) | Teks & ikon lencana poin SKPI terverifikasi (di atas #DCFCE7) |
| `status/deadline-warning`| `--status-deadline-warn` | `#B45309` | **5.0 : 1** (AA) | Teks lencana sisa kuota menipis (di atas #FEF3C7) |
| `status/error` | `--status-error` | `#DC2626` | **4.9 : 1** (AA) | Garis tepi input error & teks pesan galat validasi |
| `status/info` | `--status-info` | `#1D4ED8` | **5.3 : 1** (AA) | Garis input focused & lencana informasi (di atas #DBEAFE) |

### 5.2 Token Spasi (8pt Grid System & Gestalt Proximity)
* **Spasi Internal (`space/internal`):**
  * `--space-label-gap`: `8px` (Jarak vertikal antara label form dengan kotak input di bawahnya)
  * `--space-button-padding-v`: `12px` | `--space-button-padding-h`: `24px`
  * `--space-card-padding`: `24px` (Padding dalam pada kartu acara, sidebar, dan form)
* **Spasi Eksternal (`space/external`):**
  * `--space-form-row-gap`: `24px` (Jarak antar baris form — mematuhi aturan Internal 8px <= External 24px)
  * `--space-card-gap`: `24px` (Jarak antar kartu pada grid katalog & beranda)
  * `--space-section-gap`: `64px` / `48px` (Jarak vertikal antar seksi halaman)
* **Corner Radius & Elevation:**
  * `--radius-medium`: `8px` (Seragam untuk seluruh tombol, kartu, badge, dan kolom input)

### 5.3 Skala Tipografi Modular (Inter – Google Fonts)
* `judul-halaman`: `24px` | Bold (700) | Line-height: 120%
* `judul-bagian`: `18px` | Semibold (600) | Line-height: 130%
* `judul-kartu`: `16px` | Semibold (600) | Line-height: 130%
* `label`: `16px` | Semibold (600) | Line-height: 150%
* `teks-isi`: `16px` | Regular (400) | Line-height: 150%
* `teks-pendukung`: `14px` | Regular (400) | Line-height: 150%
* `teks-kecil`: `12px` | Semibold (600) | Line-height: 150%

---

## 6. Tech Stack Plan (Rencana Teknologi untuk Modul 7)

1. **Core Markup & Styling:**
   * HTML5 Semantik (`<header>`, `<nav>`, `<main>`, `<aside>`, `<section>`, `<article>`, `<footer>`) untuk mendukung aksesibilitas screen reader.
   * Modern CSS3 (Vanilla CSS dengan Design Tokens / Custom Variables `--*`) menerapkan CSS Grid (12 kolom) dan Flexbox yang merepresentasikan 100% Auto Layout Figma, atau opsi utilitas Tailwind CSS yang dikonfigurasi mengikuti token 01_Primitives & 02_Semantics.
2. **Interaktivitas Front-End:**
   * Vanilla JavaScript (ES6+): Digunakan untuk menangani validasi real-time 10 digit NBI pada halaman Login/Form, penyaringan (filtering) kartu kegiatan berdasarkan kategori/SKPI di Katalog, perpindahan tab riwayat tiket, serta fungsi cetak/unduh E-Tiket (window.print()).
3. **Version Control & Deployment:**
   * Git & GitHub: Kolaborasi berbasis feature/docs branch dan Pull Request Review.
   * Netlify / Vercel / GitHub Pages: Hosting dan continuous deployment untuk penayangan prototipe web langsung.
