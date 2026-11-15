PRODUCT REQUIREMENTS DOCUMENT (PRD)
UNTAG Event Hub
Atribut	Keterangan
Dokumen	PRD Gabungan — Dokumen 02 (Product Scope & User Flow) dan Dokumen 03 (Technical Architecture & UI Components)
Versi	1.2
Platform	Web Application
Target	Dokumentasi Modul 6 dan acuan implementasi Modul 7
Zona waktu aplikasi	`Asia/Jakarta`
---
Daftar Isi
Informasi Produk
Latar Belakang dan Permasalahan
Tujuan Produk
Pengguna dan Peran
Ruang Lingkup Produk
Kebutuhan Fungsional
Aturan Bisnis
User Flow
Kriteria Penerimaan
Arsitektur dan Teknologi
Struktur Data Firestore
Cloud Functions dan Proses Backend
Spesifikasi UI dan Implementasi Figma
Keamanan dan Hak Akses
Integrasi dan Konfigurasi
Pengujian
Deployment
Definition of Done
Asumsi dan Batasan
Pengembangan Berikutnya
Referensi Desain
---
1. Informasi Produk
1.1 Nama Produk
UNTAG Event Hub
1.2 Deskripsi Singkat
UNTAG Event Hub adalah aplikasi berbasis web untuk memusatkan informasi dan proses pendaftaran kegiatan mahasiswa. Aplikasi menyediakan katalog acara, informasi detail dan jadwal, pendaftaran daring, tiket elektronik dengan QR Code, riwayat keikutsertaan, serta fasilitas pengelolaan acara dan peserta bagi penyelenggara dan administrator.
1.3 Visi Produk
Menyediakan satu platform yang memudahkan mahasiswa menemukan dan mengikuti kegiatan kampus, sekaligus membantu penyelenggara mengelola acara dan kehadiran secara lebih tertib, terukur, dan transparan.
1.4 Sasaran Dokumen
Dokumen ini menggabungkan dua bagian spesifikasi:
Dokumen 02 — Product Scope & User Flow: menjelaskan ruang lingkup produk, pengguna, kebutuhan, aturan bisnis, alur pengguna, dan kriteria penerimaan.
Dokumen 03 — Technical Architecture & UI Components: menjelaskan teknologi, arsitektur, model data, proses backend, keamanan, serta spesifikasi implementasi antarmuka.
Dokumen ini menjadi acuan bersama tim selama pengembangan. Jika terjadi perbedaan antara rancangan visual dan aturan fungsional, aturan bisnis serta kebutuhan yang ditetapkan dalam dokumen ini menjadi acuan implementasi.
---
2. Latar Belakang dan Permasalahan
Informasi kegiatan mahasiswa dapat tersebar di berbagai kanal, seperti poster, grup WhatsApp, Instagram, dan pengumuman organisasi. Kondisi tersebut dapat menyebabkan mahasiswa kesulitan menemukan informasi yang lengkap, memastikan jadwal kegiatan, dan mengetahui status pendaftaran.
Di sisi penyelenggara, proses pendaftaran dan pendataan peserta yang dilakukan secara terpisah dapat menimbulkan pekerjaan administratif berulang. Pemeriksaan peserta saat kegiatan juga berisiko tidak konsisten apabila hanya mengandalkan daftar manual atau tangkapan layar bukti pendaftaran.
UNTAG Event Hub dirancang untuk mengatasi permasalahan tersebut melalui satu alur digital yang menghubungkan penemuan acara, pendaftaran, penerbitan tiket, dan pencatatan kehadiran.
2.1 Permasalahan Utama
Informasi kegiatan tersebar di banyak kanal.
Mahasiswa harus mencari ulang informasi penting seperti jadwal, lokasi, kuota, dan tenggat pendaftaran.
Proses pendaftaran belum terpusat dan status pendaftaran sulit dilacak.
Bukti pendaftaran berbentuk pesan atau tangkapan layar tidak praktis untuk diverifikasi.
Penyelenggara membutuhkan pendataan peserta, pemeriksaan tiket, dan rekap kehadiran dalam satu sistem.
Data kegiatan dan statistik perlu dibatasi berdasarkan organisasi agar tidak dapat diakses oleh penyelenggara lain.
2.2 Persona Pengguna
Persona 1 — Rania Maharani
Atribut	Deskripsi
Usia	20 tahun
Semester	5
Aktivitas	Mahasiswa yang juga memiliki kesibukan lain
Kebutuhan	Informasi acara yang lengkap, jadwal yang jelas, dan kepastian status pendaftaran
Kendala	Informasi kegiatan tersebar di WhatsApp dan Instagram
Harapan	Dapat menemukan kegiatan, memahami manfaatnya, dan mendaftar tanpa proses yang berulang
Persona 2 — Bagas Adi / Dini Anggraini
Atribut	Deskripsi
Usia	20 tahun
Fakultas	FTEIC
Semester	5
Kebutuhan	Proses pendaftaran cepat dan tiket elektronik yang mudah ditunjukkan
Kendala	Harus mencari ulang poster, membuka tautan formulir, atau mengirim ulang bukti pendaftaran ke grup
Harapan	Pendaftaran dapat diselesaikan dalam waktu singkat dan tiket dapat digunakan untuk proses check-in
2.3 Pernyataan Masalah
Mahasiswa membutuhkan platform terpusat untuk menemukan dan mendaftar kegiatan kampus tanpa harus berpindah-pindah kanal. Penyelenggara membutuhkan alat yang dapat membantu pengelolaan acara dan peserta secara efisien, dengan data yang aman dan terpisah berdasarkan organisasi.
---
3. Tujuan Produk
3.1 Tujuan untuk Mahasiswa
Menyediakan katalog kegiatan yang dapat dicari dan difilter.
Menampilkan informasi acara secara lengkap dan konsisten.
Memungkinkan pendaftaran acara secara daring.
Menerbitkan tiket elektronik dengan QR Code yang dapat diverifikasi.
Menyediakan riwayat pendaftaran dan status keikutsertaan.
Menampilkan informasi status dan poin SKPI pada acara yang relevan.
3.2 Tujuan untuk Penyelenggara
Memudahkan pembuatan dan pengelolaan acara milik organisasinya.
Menyediakan daftar peserta yang terpusat.
Mempercepat proses check-in menggunakan QR Code.
Menyediakan pencatatan kehadiran manual dengan alasan dan jejak audit.
Menampilkan statistik kegiatan milik organisasi sendiri.
Menyediakan ekspor data peserta.
3.3 Tujuan untuk Admin
Mengelola akun pengguna dan organisasi.
Memantau seluruh kegiatan dalam platform.
Menangani proses persetujuan acara.
Memantau statistik platform secara keseluruhan.
Menjaga konsistensi data dan hak akses.
3.4 Indikator Keberhasilan
Mahasiswa dapat menemukan detail acara dan menyelesaikan pendaftaran melalui satu alur.
Tiket elektronik diterbitkan setelah pendaftaran berhasil.
QR Code hanya dapat digunakan untuk check-in satu kali.
Penyelenggara hanya dapat mengakses data organisasi yang menjadi tanggung jawabnya.
Data peserta dan kehadiran dapat ditampilkan serta diekspor secara konsisten.
---
4. Pengguna dan Peran
UNTAG Event Hub memiliki tiga peran utama.
4.1 Mahasiswa
Mahasiswa merupakan pengguna yang mencari dan mengikuti kegiatan.
Hak akses utama:
Melihat beranda dan katalog acara.
Melihat detail acara, jadwal, lokasi, kuota, biaya, serta informasi SKPI.
Mendaftar acara yang masih tersedia.
Melihat tiket dan QR Code miliknya.
Mengunduh tiket.
Melihat riwayat kegiatan.
Membatalkan pendaftaran sesuai ketentuan.
4.2 Penyelenggara
Penyelenggara merupakan pengelola kegiatan yang terikat pada satu organisasi.
Hak akses utama:
Membuat dan mengelola acara milik organisasinya.
Melihat daftar peserta acara milik organisasinya.
Memindai QR Code tiket untuk check-in.
Melakukan pencatatan kehadiran manual dengan alasan.
Melihat statistik kegiatan milik organisasinya.
Mengekspor data peserta.
Penyelenggara tidak boleh melihat atau mengubah data organisasi lain.
4.3 Admin
Admin merupakan pengelola platform dengan cakupan akses lintas organisasi.
Hak akses utama:
Mengelola akun pengguna.
Mengelola organisasi.
Memantau dan mengelola seluruh acara.
Menyetujui atau menolak acara yang membutuhkan persetujuan.
Melihat statistik keseluruhan platform.
Memantau aktivitas penting melalui audit log.
4.4 Matriks Hak Akses
Fitur	Mahasiswa	Penyelenggara	Admin
Melihat katalog acara	Ya	Ya	Ya
Melihat detail acara	Ya	Ya	Ya
Mendaftar acara	Ya	Tidak	Tidak
Melihat tiket pribadi	Ya	Tidak	Tidak
Membatalkan pendaftaran sendiri	Ya	Tidak	Tidak
Membuat acara	Tidak	Ya	Ya
Mengubah acara	Tidak	Acara organisasi sendiri	Semua acara sesuai kewenangan
Melihat peserta	Tidak	Acara organisasi sendiri	Semua acara
Memindai tiket/check-in	Tidak	Acara organisasi sendiri	Sesuai kewenangan
Mengubah kehadiran manual	Tidak	Acara organisasi sendiri	Sesuai kewenangan
Melihat statistik	Tidak	Organisasi sendiri	Seluruh platform
Mengelola pengguna dan organisasi	Tidak	Tidak	Ya
Menyetujui acara	Tidak	Tidak	Ya
---
5. Ruang Lingkup Produk
5.1 Fitur dalam MVP
Modul	Fitur	Deskripsi
Autentikasi	Login	Login menggunakan NBI atau email dan password
Autentikasi	Google Sign-In	Login menggunakan akun Google
Profil	Data mahasiswa	Menyimpan identitas mahasiswa, termasuk NBI
Beranda	Ringkasan acara	Menampilkan acara pilihan dan informasi utama
Katalog	Daftar acara	Menampilkan acara yang tersedia
Katalog	Filter	Filter status SKPI, kategori, dan bulan
Detail acara	Informasi acara	Deskripsi, penyelenggara, lokasi, jadwal, kuota, dan biaya
Detail acara	Informasi SKPI	Status dan poin SKPI jika tersedia
Pendaftaran	Registrasi gratis	Mahasiswa dapat mendaftar acara tanpa pembayaran
Tiket	E-ticket	Penerbitan tiket elektronik setelah pendaftaran berhasil
Tiket	QR Code	QR unik untuk verifikasi tiket
Tiket	Unduh PDF	Mengunduh tiket elektronik
Riwayat	Daftar tiket	Menampilkan pendaftaran mendatang dan kegiatan selesai
Riwayat	Pembatalan	Membatalkan pendaftaran sesuai aturan
Penyelenggara	Manajemen acara	Membuat dan mengelola acara organisasi
Penyelenggara	Manajemen peserta	Melihat dan mengekspor daftar peserta
Penyelenggara	Check-in	Memindai QR Code dan mencatat kehadiran
Penyelenggara	Statistik	Statistik kegiatan organisasi sendiri
Admin	Manajemen platform	Mengelola pengguna, organisasi, dan acara
Admin	Persetujuan	Menyetujui atau menolak acara
5.2 Di Luar MVP
Fitur berikut tidak menjadi kewajiban pada implementasi MVP:
Pembayaran tiket berbayar dan integrasi payment gateway.
Integrasi API otomatis dengan SIMPOINT.
Sinkronisasi otomatis poin SKPI ke sistem eksternal.
Aplikasi mobile native.
Rekomendasi acara berbasis machine learning.
Notifikasi WhatsApp otomatis.
Integrasi kalender eksternal.
Analitik lanjutan di luar statistik dasar yang ditentukan.
5.3 Prinsip Batasan MVP
MVP berfokus pada alur inti: menemukan acara, membaca detail, mendaftar, memperoleh tiket, dan melakukan check-in. Fitur tambahan tidak boleh menghambat penyelesaian alur inti tersebut.
5.4 Ketentuan SKPI pada MVP
Informasi SKPI tetap termasuk dalam MVP dengan batasan berikut:
Katalog dan detail acara dapat menampilkan status SKPI dan jumlah poin jika informasi tersebut tersedia.
Label kategori atau jenis poin SKPI dapat ditampilkan, misalnya 15 Poin SKPI — Penalaran.
Halaman detail acara dapat menyediakan tautan eksternal menuju SIMPOINT.
Penetapan atau perubahan poin tetap mengikuti data dan proses yang ditentukan pihak berwenang.
Integrasi API otomatis dengan SIMPOINT, termasuk pengiriman atau sinkronisasi poin secara langsung, berada di luar MVP.
---
6. Kebutuhan Fungsional
6.1 Autentikasi dan Profil
Sistem menyediakan login menggunakan NBI atau email beserta password.
Sistem menyediakan Google Sign-In.
Sistem memvalidasi format NBI sesuai ketentuan kampus.
Sistem menghubungkan akun yang berhasil login dengan dokumen profil pengguna.
Pengguna memiliki role yang menentukan akses halaman dan operasi.
Sistem tidak memperbolehkan pengguna menentukan atau menaikkan role sendiri melalui antarmuka klien.
6.2 Katalog dan Detail Acara
Sistem menampilkan daftar acara yang berstatus dapat ditampilkan kepada mahasiswa.
Mahasiswa dapat mencari acara berdasarkan kata kunci.
Mahasiswa dapat memfilter acara berdasarkan status SKPI, kategori, dan bulan.
Sistem menampilkan informasi acara, penyelenggara, jadwal, lokasi, kuota, biaya, dan tenggat pendaftaran.
Sistem mengurutkan acara berdasarkan tenggat pendaftaran terdekat sebagai urutan awal.
Sistem menampilkan Empty State apabila tidak ada acara yang sesuai dengan pencarian atau filter.
6.3 Pendaftaran
Mahasiswa yang sudah login dapat mendaftar acara yang memenuhi syarat.
Sistem memvalidasi status acara, tenggat pendaftaran, kuota, dan pendaftaran duplikat.
Sistem memvalidasi kuota acara dan sesi jika acara menggunakan sesi.
Pendaftaran yang berhasil menghasilkan satu data registrasi dan tiket.
Sistem menolak pendaftaran apabila acara sudah penuh, ditutup, atau pengguna telah terdaftar.
6.4 Tiket Elektronik
Setiap pendaftaran berhasil memiliki tiket unik.
Tiket menampilkan identitas acara dan informasi peserta yang diperlukan.
QR Code berisi token acak yang aman dan tidak menggunakan UID pengguna atau nomor urut pendaftaran sebagai token.
Tiket dapat dilihat dari halaman sukses maupun riwayat tiket.
Tiket dapat diunduh dalam format PDF.
Token tiket hanya berlaku untuk registrasi yang terkait dan tidak dapat dipakai untuk registrasi lain.
6.5 Riwayat dan Pembatalan
Mahasiswa dapat melihat tiket yang akan datang dan kegiatan yang telah selesai diikuti.
Mahasiswa dapat melihat status registrasi dan kehadiran.
Pembatalan hanya dapat dilakukan paling lambat 24 jam sebelum acara dimulai.
Pembatalan yang berhasil mengubah status registrasi dan mengembalikan kuota satu kali.
Registrasi yang sudah dibatalkan tidak boleh mengembalikan kuota berulang kali jika permintaan pembatalan dikirim ulang.
6.6 Pengelolaan Acara oleh Penyelenggara
Penyelenggara dapat membuat acara untuk organisasi yang menjadi tanggung jawabnya.
Penyelenggara dapat melihat dan mengubah acara milik organisasinya.
Penyelenggara tidak dapat mengubah `organizationId` untuk mengambil alih acara organisasi lain.
Perubahan acara yang telah dipublikasikan mengikuti aturan pada bagian Aturan Bisnis.
Sistem mencatat perubahan penting ke audit log.
6.7 Pengelolaan Peserta dan Kehadiran
Penyelenggara dapat melihat peserta acara organisasinya.
Penyelenggara dapat memindai QR Code untuk memverifikasi tiket.
QR Code yang valid hanya dapat digunakan satu kali untuk check-in.
Penyelenggara dapat melakukan pencatatan kehadiran manual dengan alasan.
Perubahan kehadiran manual dicatat dalam audit log.
Sistem menyediakan ekspor data peserta dalam format CSV melalui proses backend yang memverifikasi hak akses.
6.8 Statistik
Dashboard penyelenggara hanya menampilkan statistik kegiatan milik organisasinya.
Dashboard admin dapat menampilkan statistik lintas organisasi.
Statistik penyelenggara dihitung berdasarkan data kegiatan dan peserta yang berada dalam cakupan organisasinya.
Statistik tidak boleh mengambil data organisasi lain.
---
7. Aturan Bisnis
7.1 Status Acara
Status acara yang digunakan harus konsisten di seluruh aplikasi.
Status	Makna
`draft`	Acara masih disusun dan belum ditampilkan kepada mahasiswa
`pending_approval`	Acara menunggu persetujuan admin
`published`	Acara telah disetujui dan dapat ditampilkan sesuai jadwal publikasi
`rejected`	Acara ditolak oleh admin
`cancelled`	Acara dibatalkan
`completed`	Acara telah selesai
Status yang ditampilkan kepada pengguna dapat menggunakan label Bahasa Indonesia, sedangkan nilai yang disimpan di database menggunakan nilai enum yang konsisten.
7.2 Persetujuan Acara
Acara yang membutuhkan persetujuan harus melalui status `pending_approval`.
Admin dapat menyetujui atau menolak acara.
Acara yang ditolak tidak ditampilkan sebagai acara aktif kepada mahasiswa.
Keputusan persetujuan dan identitas admin dicatat dalam data persetujuan serta audit log.
7.3 Perubahan Acara Setelah Dipublikasikan
Perubahan berikut diperbolehkan tanpa mengulang proses persetujuan, selama tidak mengubah identitas dan tujuan utama kegiatan:
Deskripsi acara.
Poster.
Informasi tambahan.
Penambahan kuota.
Jadwal acara.
Lokasi acara.
Ketentuan:
Acara tetap berstatus `published` setelah perubahan yang diizinkan.
Setiap perubahan harus dicatat dalam audit log.
Kuota tidak boleh diturunkan di bawah jumlah pendaftar aktif.
Perubahan jadwal harus ditampilkan secara jelas kepada pengguna.
Perubahan yang secara substansial mengubah identitas, penyelenggara, atau tujuan acara dapat memerlukan peninjauan admin.
7.4 Kuota Acara dan Sesi
Acara dapat memiliki satu atau beberapa sesi.
Jika acara tidak menggunakan sesi, kuota dikelola pada tingkat acara.
Jika acara menggunakan sesi, kuota sesi menjadi batas kapasitas untuk sesi yang dipilih.
Sistem harus memeriksa kapasitas acara dan sesi dalam satu transaksi backend.
Jumlah peserta tidak boleh melebihi kuota yang berlaku.
Pengembalian kuota akibat pembatalan harus dilakukan tepat satu kali.
7.5 Pembatalan Pendaftaran
Mahasiswa hanya dapat membatalkan pendaftaran miliknya sendiri.
Pembatalan hanya diperbolehkan paling lambat 24 jam sebelum waktu mulai acara.
Sistem mengubah status registrasi menjadi `cancelled`.
Sistem menonaktifkan token tiket terkait.
Kuota dikembalikan dalam transaksi yang sama.
Permintaan pembatalan berulang harus bersifat idempotent.
7.6 Token QR dan Check-in
Token QR dibuat menggunakan sumber acak yang aman secara kriptografis.
Token tidak boleh berupa UID pengguna, NBI, atau nomor registrasi berurutan.
Token disimpan dalam bentuk hash atau mekanisme aman yang setara.
Verifikasi dilakukan melalui Cloud Function.
Tiket harus berstatus valid dan belum pernah digunakan.
Proses verifikasi dan pencatatan check-in harus atomik agar dua pemindaian bersamaan tidak menghasilkan check-in ganda.
Token yang sudah digunakan, dibatalkan, tidak dikenal, atau tidak sesuai acara harus ditolak.
7.7 Status Kehadiran
Status kehadiran setidaknya mencakup:
Status	Makna
`registered`	Sudah terdaftar, belum check-in
`attended`	Kehadiran berhasil dicatat
`absent`	Acara selesai dan peserta tidak memiliki catatan kehadiran
`cancelled`	Pendaftaran dibatalkan
Setelah acara selesai, registrasi yang tidak memiliki catatan check-in dapat ditandai `absent` melalui proses backend. Perubahan manual harus memiliki alasan dan jejak audit.
7.8 Aturan Statistik Penyelenggara
Statistik penyelenggara hanya mencakup kegiatan yang dimiliki organisasi penyelenggara tersebut. Statistik tidak boleh menampilkan agregat lintas organisasi, termasuk melalui query langsung atau endpoint ekspor.
---
8. User Flow
8.1 Alur Mahasiswa
Mahasiswa membuka aplikasi.
Mahasiswa login menggunakan NBI atau email dan password, atau Google Sign-In.
Sistem memuat profil dan role mahasiswa.
Mahasiswa melihat beranda atau membuka katalog.
Mahasiswa mencari atau memfilter acara.
Mahasiswa membuka detail acara.
Mahasiswa memilih sesi jika acara menyediakan pilihan sesi.
Mahasiswa mengisi atau mengonfirmasi data pendaftaran.
Sistem memvalidasi persyaratan dan kapasitas.
Jika valid, sistem menyimpan registrasi dan membuat tiket.
Mahasiswa melihat halaman sukses dan QR Code.
Tiket dapat dibuka kembali melalui riwayat atau diunduh sebagai PDF.
8.2 Alur Check-in
Penyelenggara login.
Penyelenggara membuka acara milik organisasinya.
Penyelenggara membuka fitur pemindaian.
QR Code peserta dipindai.
Sistem mengirim token ke backend untuk diverifikasi.
Backend memeriksa token, registrasi, acara, dan status check-in.
Jika valid dan belum digunakan, sistem mencatat kehadiran.
Sistem menampilkan hasil berhasil atau alasan penolakan.
8.3 Alur Persetujuan Acara
Penyelenggara membuat acara.
Acara disimpan sebagai draft atau dikirim untuk persetujuan.
Jika persetujuan diperlukan, status berubah menjadi `pending_approval`.
Admin memeriksa detail acara.
Admin menyetujui atau menolak.
Sistem menyimpan keputusan dan audit log.
Acara yang disetujui dapat dipublikasikan sesuai aturan.
8.4 Alur Pembatalan Pendaftaran
Mahasiswa membuka riwayat tiket.
Mahasiswa memilih pendaftaran yang akan dibatalkan.
Sistem memeriksa kepemilikan registrasi dan batas waktu 24 jam.
Jika memenuhi syarat, backend membatalkan registrasi dan menonaktifkan tiket.
Backend mengembalikan kuota satu kali.
Sistem menampilkan status pembatalan.
---
9. Kriteria Penerimaan
9.1 Autentikasi
Pengguna dapat login menggunakan email dan password yang valid.
Pengguna dapat login menggunakan NBI dan password melalui mekanisme resolver yang aman.
Pengguna dapat menggunakan Google Sign-In.
NBI dengan format tidak sesuai ditolak dan pesan validasi ditampilkan.
Pengguna tidak dapat mengubah role melalui permintaan dari klien.
9.2 Katalog dan Detail
Katalog menampilkan acara yang dapat diakses mahasiswa.
Filter kategori, bulan, dan SKPI bekerja sesuai data.
Acara diurutkan berdasarkan tenggat pendaftaran terdekat.
Detail acara menampilkan informasi penting dan informasi SKPI jika tersedia.
Empty State tampil ketika hasil pencarian kosong.
9.3 Pendaftaran dan Tiket
Pendaftaran berhasil menghasilkan satu registrasi dan satu tiket.
Pendaftaran duplikat ditolak.
Pendaftaran saat kuota penuh ditolak.
QR Code tidak menggunakan UID atau ID berurutan sebagai token.
Tiket dapat dibuka kembali dan diunduh.
9.4 Check-in
QR valid dapat digunakan untuk check-in satu kali.
QR yang telah digunakan ditolak pada pemindaian berikutnya.
QR tidak valid atau milik acara lain ditolak.
Check-in yang berhasil tercatat pada data kehadiran.
Check-in ganda akibat permintaan bersamaan tidak diperbolehkan.
9.5 Hak Akses
Penyelenggara hanya dapat melihat dan mengelola acara organisasinya.
Penyelenggara tidak dapat membaca daftar peserta organisasi lain.
Statistik penyelenggara hanya menghitung data organisasi sendiri.
Admin memiliki akses lintas organisasi sesuai kewenangannya.
---
10. Arsitektur dan Teknologi
10.1 Arsitektur Umum
UNTAG Event Hub menggunakan pendekatan Backend as a Service (BaaS) dengan Firebase untuk mengurangi kebutuhan pengelolaan server khusus.
Lapisan	Teknologi	Tanggung Jawab
Frontend	React.js	Antarmuka aplikasi
Routing	React Router	Navigasi halaman dan proteksi route
Styling	Tailwind CSS	Sistem styling dan responsivitas
Authentication	Firebase Authentication	Autentikasi akun
Database	Cloud Firestore	Penyimpanan data aplikasi
Backend logic	Firebase Cloud Functions	Validasi dan proses yang membutuhkan hak istimewa
File storage	Firebase Storage	Penyimpanan poster dan aset acara
Hosting	Vercel	Deployment frontend
Version control	GitHub	Pengelolaan source code dan kolaborasi
10.2 Prinsip Arsitektur
Frontend bertanggung jawab atas presentasi dan interaksi pengguna.
Operasi sensitif harus dijalankan melalui Cloud Functions.
Firestore Security Rules menjadi lapisan perlindungan akses data.
Hak akses ditentukan berdasarkan role dan kepemilikan organisasi.
Validasi penting tidak boleh hanya mengandalkan validasi frontend.
Operasi yang mengubah beberapa dokumen terkait harus menggunakan transaksi atau mekanisme atomik yang sesuai.
10.3 Struktur Route
Route	Akses	Halaman
`/login`	Publik	Login
`/`	Mahasiswa	Beranda
`/events`	Mahasiswa	Katalog
`/events/:eventId`	Mahasiswa	Detail acara
`/events/:eventId/register`	Mahasiswa	Form pendaftaran
`/tickets/success/:registrationId`	Pemilik tiket	Sukses tiket
`/tickets`	Mahasiswa	Riwayat tiket
`/organizer`	Penyelenggara	Dashboard penyelenggara
`/organizer/events`	Penyelenggara	Daftar acara organisasi
`/organizer/events/:eventId`	Penyelenggara	Detail dan pengelolaan acara
`/organizer/events/:eventId/participants`	Penyelenggara	Daftar peserta
`/organizer/events/:eventId/check-in`	Penyelenggara	Pemindaian tiket
`/admin`	Admin	Dashboard admin
`/admin/users`	Admin	Manajemen pengguna
`/admin/organizations`	Admin	Manajemen organisasi
`/admin/events`	Admin	Manajemen dan persetujuan acara
Route yang dilindungi harus memeriksa status autentikasi dan role. Pemeriksaan di frontend hanya untuk pengalaman pengguna; backend dan Security Rules tetap menjadi otoritas keamanan.
---
11. Struktur Data Firestore
11.1 Koleksi Utama
Koleksi	Fungsi
`users`	Profil pengguna dan role
`organizations`	Data organisasi
`events`	Data acara
`registrations`	Data pendaftaran peserta
`nbi_registry`	Referensi NBI yang sah jika sumber data tersedia
`ticket_tokens`	Data token tiket untuk verifikasi
`event_approvals`	Riwayat persetujuan acara
`attendance_history`	Riwayat perubahan kehadiran
`audit_logs`	Catatan aktivitas penting
11.2 `users`
Dokumen disimpan menggunakan UID Firebase Authentication sebagai document ID.
```json
{
  "uid": "firebase-auth-uid",
  "name": "Nama Pengguna",
  "email": "user@example.com",
  "nbi": "10 digit NBI",
  "role": "student",
  "organizationId": null,
  "createdAt": "timestamp",
  "updatedAt": "timestamp"
}
```
Nilai `role` yang diperbolehkan antara lain `student`, `organizer`, dan `admin`. Penetapan role dilakukan melalui proses backend yang berwenang.
11.3 `organizations`
```json
{
  "name": "Nama Organisasi",
  "description": "Deskripsi organisasi",
  "logoUrl": "https://...",
  "status": "active",
  "createdAt": "timestamp",
  "updatedAt": "timestamp"
}
```
11.4 `events`
```json
{
  "title": "Nama Acara",
  "slug": "nama-acara",
  "description": "Deskripsi acara",
  "posterUrl": "https://...",
  "category": "seminar",
  "organizationId": "organization-document-id",
  "status": "published",
  "location": "Lokasi acara",
  "startAt": "timestamp",
  "endAt": "timestamp",
  "registrationDeadline": "timestamp",
  "quota": 100,
  "registeredCount": 0,
  "fee": 0,
  "skpi": {
    "status": "verified",
    "category": "Penalaran",
    "points": 15,
    "simpointUrl": "https://..."
  },
  "usesSessions": false,
  "createdAt": "timestamp",
  "updatedAt": "timestamp"
}
```
11.5 Subkoleksi `events/{eventId}/sessions`
Acara yang menyediakan pilihan sesi menggunakan subkoleksi `sessions`.
```json
{
  "name": "Sesi Pagi",
  "startAt": "timestamp",
  "endAt": "timestamp",
  "quota": 50,
  "registeredCount": 0,
  "status": "active",
  "createdAt": "timestamp",
  "updatedAt": "timestamp"
}
```
`sessionId` disimpan pada dokumen registrasi yang memilih sesi tersebut. Untuk acara tanpa sesi, `sessionId` bernilai `null`.
11.6 `registrations`
```json
{
  "eventId": "event-document-id",
  "sessionId": "session-document-id-or-null",
  "userId": "firebase-auth-uid",
  "ticketId": "UNTAG-2026-RANDOMSUFFIX",
  "status": "registered",
  "attendanceStatus": "registered",
  "registeredAt": "timestamp",
  "cancelledAt": null,
  "createdAt": "timestamp",
  "updatedAt": "timestamp"
}
```
11.7 `ticket_tokens`
```json
{
  "registrationId": "registration-document-id",
  "eventId": "event-document-id",
  "tokenHash": "secure-hash-of-random-token",
  "status": "active",
  "usedAt": null,
  "createdAt": "timestamp"
}
```
Token mentah hanya diberikan kepada pengguna yang berhak ketika tiket dibuat atau ditampilkan. Token mentah tidak disimpan sebagai nilai yang dapat dibaca publik di Firestore.
11.8 `event_approvals`
```json
{
  "eventId": "event-document-id",
  "reviewerId": "admin-uid",
  "decision": "approved",
  "notes": "Catatan admin",
  "reviewedAt": "timestamp"
}
```
11.9 `attendance_history`
```json
{
  "registrationId": "registration-document-id",
  "eventId": "event-document-id",
  "userId": "firebase-auth-uid",
  "action": "check_in",
  "previousStatus": "registered",
  "newStatus": "attended",
  "reason": null,
  "actorId": "organizer-uid",
  "createdAt": "timestamp"
}
```
11.10 `audit_logs`
```json
{
  "actorId": "firebase-auth-uid",
  "actorRole": "organizer",
  "organizationId": "organization-document-id",
  "action": "event_updated",
  "targetType": "event",
  "targetId": "event-document-id",
  "metadata": {},
  "createdAt": "timestamp"
}
```
Audit log harus dibuat oleh backend dan tidak dapat diubah oleh pengguna biasa.
11.11 Catatan Konsistensi Data
Gunakan `Timestamp` Firestore untuk nilai waktu, bukan string tanggal bebas.
Gunakan UID Firebase Authentication sebagai referensi identitas internal.
Field `organizationId` harus diverifikasi dari data pengguna yang terautentikasi.
Nilai penghitung kuota tidak boleh diubah langsung oleh frontend.
Operasi registrasi dan pembatalan harus menjaga konsistensi penghitung kuota.
Struktur indeks Firestore harus disesuaikan dengan query katalog, riwayat, dan dashboard.
---
12. Cloud Functions dan Proses Backend
12.1 Daftar Cloud Functions
Function	Tanggung Jawab
`completeStudentProfile`	Melengkapi profil mahasiswa setelah autentikasi
`assignUserRole`	Menetapkan role oleh aktor yang berwenang
`resolveNbiLogin`	Menyelesaikan login NBI melalui resolver server yang aman
`registerForEvent`	Memvalidasi dan membuat registrasi serta tiket
`cancelRegistration`	Membatalkan registrasi dan mengembalikan kuota
`approveEvent`	Menyetujui atau menolak acara
`updateEvent`	Memvalidasi perubahan acara dan mencatat audit
`cancelEvent`	Membatalkan acara dan menangani status registrasi terkait
`verifyTicket`	Memverifikasi token QR dan mencatat check-in
`updateAttendanceManually`	Mengubah kehadiran secara manual dengan alasan
`exportParticipants`	Menghasilkan ekspor peserta setelah otorisasi
12.2 Login Menggunakan NBI atau Email
Firebase Authentication mendukung autentikasi email/password dan penyedia identitas seperti Google. Firebase Authentication tidak menyediakan login username NBI secara native. Karena itu, login NBI memerlukan resolver di sisi server.
Alur yang disarankan:
Pengguna memasukkan NBI atau email beserta password.
Frontend mengirim kredensial melalui koneksi HTTPS ke endpoint autentikasi yang terlindungi.
Jika input berupa NBI, backend memvalidasi format dan mencari pemetaan NBI ke akun email Firebase yang sesuai melalui sumber data yang terlindungi.
Backend meneruskan proses autentikasi ke mekanisme Firebase Authentication yang sesuai, tanpa mengirimkan password ke layanan pencarian NBI.
Setelah kredensial diverifikasi, pengguna memperoleh sesi Firebase yang valid.
Aplikasi memuat profil dan role dari sumber data tepercaya.
Catatan implementasi penting:
Jangan membuat login NBI dengan cara hanya mencari NBI di Firestore lalu menganggap pengguna sudah terautentikasi.
Jangan mengirim daftar pemetaan NBI dan email ke frontend.
Jangan menyimpan password dalam Firestore atau log.
Terapkan rate limiting dan perlindungan terhadap brute force.
Gunakan pesan kegagalan generik agar endpoint tidak membocorkan apakah NBI atau email tertentu terdaftar.
Gunakan mekanisme token atau custom authentication yang sesuai dengan kemampuan Firebase dan implementasi backend.
Implementasi harus diuji menyeluruh sebelum login NBI diaktifkan pada lingkungan produksi.
Jika sumber data NBI resmi belum tersedia, fitur login NBI harus menggunakan data pemetaan yang telah diverifikasi dan dikelola secara aman. Jangan mengarang atau mengisi data NBI yang tidak sah.
12.3 `registerForEvent`
Proses pendaftaran harus dijalankan di backend dengan transaksi:
Memastikan pengguna telah terautentikasi.
Memastikan role pengguna adalah mahasiswa.
Memastikan acara tersedia dan berstatus `published`.
Memastikan tenggat pendaftaran belum terlewati.
Memastikan pengguna belum memiliki registrasi aktif untuk acara tersebut.
Jika acara menggunakan sesi, memvalidasi sesi dan kuotanya.
Memeriksa kuota acara dan sesi sesuai aturan kapasitas.
Membuat dokumen registrasi.
Membuat ticket ID dan token QR acak.
Menyimpan hash token.
Memperbarui penghitung kuota secara atomik.
Mengembalikan data tiket yang diperlukan kepada pengguna.
Seluruh perubahan yang saling bergantung harus berhasil sebagai satu operasi atomik. Jika validasi atau penulisan gagal, tidak boleh ada registrasi parsial atau penghitung kuota yang berubah tanpa registrasi.
12.4 `cancelRegistration`
Memastikan pemanggil adalah pemilik registrasi atau aktor berwenang.
Memastikan registrasi masih aktif.
Memastikan pembatalan dilakukan paling lambat 24 jam sebelum acara dimulai.
Mengubah status registrasi menjadi `cancelled`.
Menonaktifkan token tiket.
Mengurangi penghitung peserta acara dan sesi yang relevan tepat satu kali.
Mencatat waktu pembatalan dan audit yang diperlukan.
12.5 `verifyTicket`
Menerima token QR dan konteks acara.
Menghitung hash token untuk pencarian.
Memastikan token ditemukan dan berstatus aktif.
Memastikan registrasi masih valid dan sesuai acara.
Memastikan tiket belum pernah digunakan.
Mencatat waktu check-in dan aktor.
Mengubah status kehadiran menjadi `attended`.
Menandai token sebagai telah digunakan.
Mengembalikan hasil verifikasi yang tidak membocorkan data pribadi berlebihan.
Pemeriksaan dan perubahan status harus dilakukan secara transaksional untuk mencegah penggunaan token yang sama secara bersamaan.
12.6 `updateAttendanceManually`
Hanya aktor yang berwenang untuk acara tersebut yang dapat mengubah status.
Alasan perubahan wajib diisi.
Status sebelum dan sesudah perubahan disimpan.
Identitas aktor dan waktu perubahan dicatat.
Perubahan tidak boleh menghapus riwayat sebelumnya.
12.7 `exportParticipants`
Backend memverifikasi role dan cakupan organisasi.
Penyelenggara hanya dapat mengekspor peserta acara organisasinya.
Admin dapat mengekspor sesuai kewenangannya.
File CSV hanya berisi kolom yang diperlukan.
URL unduhan, jika menggunakan file sementara, harus memiliki masa berlaku terbatas.
12.8 Format Ticket ID
Ticket ID merupakan identitas tampilan tiket dan berbeda dari token QR.
Format yang disarankan:
```text
UNTAG-{YEAR}-{RANDOM_SUFFIX}
```
Contoh tampilan:
```text
UNTAG-2026-8F3K2M
```
`RANDOM_SUFFIX` harus dihasilkan menggunakan sumber acak yang aman dan diperiksa keunikannya. Contoh `#UNTAG-2026-0891` pada desain Figma hanya merupakan contoh visual, bukan ketentuan bahwa ID produksi harus berurutan. Ticket ID tidak boleh digunakan sebagai token autentikasi atau token QR.
---
13. Spesifikasi UI dan Implementasi Figma
13.1 Prinsip Desain
Antarmuka harus:
Bersih, mudah dipahami, dan konsisten.
Mengutamakan hierarki informasi yang jelas.
Responsif pada desktop, tablet, dan perangkat mobile.
Menggunakan komponen yang konsisten.
Menghindari penggunaan pill berlebihan.
Menghindari sudut terlalu membulat pada seluruh elemen.
Menghindari gradien, bayangan, dan dekorasi yang tidak memiliki fungsi.
Memprioritaskan keterbacaan, aksesibilitas, dan kejelasan status.
13.2 Delapan Frame Utama Figma
Implementasi mahasiswa harus mengikuti delapan frame utama yang telah ditentukan pada desain Figma. Dashboard penyelenggara dan admin merupakan halaman tambahan untuk mendukung fungsi produk dan bukan bagian dari delapan frame utama tersebut.
Frame 01 — `01_Login`
Komponen dan perilaku:
Form login.
Input NBI atau email.
Input password.
Tombol masuk.
Opsi Google Sign-In.
Validasi input dan pesan kesalahan.
Navigasi menuju halaman yang sesuai setelah autentikasi berhasil.
Login NBI dan email menggunakan satu field identitas. Backend menentukan apakah input berupa NBI atau email dan menjalankan proses autentikasi yang sesuai.
Frame 02 — `02_Login_Error`
Frame ini memperlihatkan keadaan validasi input yang tidak sesuai.
Contoh keadaan desain:
Input `14622001` berisi 8 digit.
Border input berubah menjadi merah.
Pesan validasi: NBI harus 10 digit.
Tombol masuk dalam keadaan nonaktif selama input tidak valid.
Validasi format NBI di frontend bertujuan membantu pengguna. Backend tetap wajib melakukan validasi ulang.
Frame 03 — `03_Beranda`
Komponen:
Navbar dan identitas aplikasi.
Hero banner dengan visual auditorium.
Ringkasan atau ajakan untuk menemukan acara.
Tiga kartu acara sebagai konten contoh pada rancangan.
Informasi utama acara dan label SKPI jika tersedia.
Akses menuju katalog.
Jumlah kartu pada desain merupakan contoh tampilan; data produksi harus berasal dari Firestore.
Frame 04 — `04_Katalog`
Komponen:
Judul halaman katalog.
Filter status SKPI.
Filter kategori.
Filter bulan.
Kumpulan kartu acara.
Tata letak kartu dua kolom pada viewport yang sesuai.
Urutan awal berdasarkan tenggat pendaftaran terdekat.
Empty State ketika hasil filter tidak ditemukan.
Filter kategori dapat menggunakan chip atau kontrol ringkas sesuai desain, tetapi tidak perlu menerapkan gaya pill secara berlebihan.
Frame 05 — `05_Detail_Acara`
Komponen:
Poster acara.
Nama acara.
Identitas penyelenggara.
Deskripsi.
Jadwal dan lokasi.
Informasi kuota dan biaya.
Status serta poin SKPI jika tersedia.
Tautan eksternal SIMPOINT.
Kartu pilihan sesi jika acara menyediakan sesi.
Tombol pendaftaran.
Status atau label SKPI yang ditampilkan harus berasal dari data acara. Tautan SIMPOINT mengarah ke sistem eksternal; tidak berarti aplikasi telah terintegrasi otomatis dengan API SIMPOINT.
Frame 06 — `06_Form_Pendaftaran`
Komponen:
Stepper tiga tahap sesuai rancangan.
Formulir dengan tata letak dua kolom pada layar yang cukup lebar.
Label dan field dengan jarak visual konsisten; acuan jarak label ke field adalah 8 px.
Ringkasan acara dan sesi yang dipilih.
Checkbox persetujuan.
Validasi field wajib.
Tombol untuk melanjutkan atau mengirim pendaftaran.
Pada layar kecil, form dua kolom harus berubah menjadi satu kolom agar tetap mudah digunakan.
Frame 07 — `07_Sukses_Tiket`
Komponen:
Ikon atau ilustrasi status berhasil.
Informasi bahwa pendaftaran sukses.
Kartu tiket elektronik.
Ticket ID.
Informasi acara dan peserta yang diperlukan.
QR Code dari token tiket yang valid.
Tombol unduh PDF.
Navigasi menuju riwayat tiket.
Contoh `#UNTAG-2026-0891` merupakan data visual pada desain. Implementasi harus menggunakan Ticket ID unik hasil backend dan QR token acak.
Frame 08 — `08_Riwayat_Tiket`
Komponen:
Tab Akan Datang dan Selesai Diikuti.
Kartu tiket.
Informasi acara dan status.
Tombol Lihat QR Tiket untuk tiket yang masih valid.
Informasi pembatalan atau kehadiran sesuai status registrasi.
Angka pada tab, seperti Akan Datang (2) dan Selesai Diikuti (3), merupakan contoh data desain. Implementasi harus menghitung jumlah berdasarkan data aktual pengguna.
13.3 Halaman Tambahan Penyelenggara dan Admin
Halaman berikut diperlukan untuk melengkapi kebutuhan produk, tetapi tidak termasuk delapan frame utama Figma:
Dashboard penyelenggara.
Daftar dan formulir pengelolaan acara.
Detail acara dan daftar peserta.
Halaman pemindaian QR/check-in.
Statistik organisasi.
Dashboard admin.
Manajemen pengguna dan organisasi.
Daftar persetujuan acara.
Halaman tambahan harus mengikuti sistem visual yang sama dengan delapan frame utama.
13.4 Komponen UI yang Disarankan
Komponen	Kegunaan
`Navbar`	Navigasi utama
`EventCard`	Ringkasan acara
`EventFilter`	Filter katalog
`EventDetail`	Informasi detail acara
`SkpiBadge`	Status atau kategori SKPI
`SessionSelector`	Pilihan sesi acara
`RegistrationStepper`	Tahapan pendaftaran
`RegistrationForm`	Form pendaftaran
`TicketCard`	Tampilan tiket
`QRCodeDisplay`	QR Code tiket
`TicketHistoryTabs`	Pemisah riwayat
`EmptyState`	Tampilan tanpa data
`LoadingState`	Indikator pemuatan
`ErrorState`	Tampilan kesalahan
`ProtectedRoute`	Pembatasan halaman berdasarkan autentikasi dan role
Komponen harus dapat digunakan ulang agar konsistensi visual dan perilaku tetap terjaga.
---
14. Keamanan dan Hak Akses
14.1 Autentikasi
Gunakan Firebase Authentication untuk pengelolaan identitas.
Jangan menyimpan password sendiri di Firestore.
Lindungi halaman berdasarkan status autentikasi dan role.
Validasi sesi dan token pada backend untuk operasi sensitif.
14.2 Otorisasi
Role pengguna harus berasal dari sumber tepercaya.
Penetapan role hanya boleh dilakukan oleh proses backend yang berwenang.
Pengguna tidak boleh menaikkan hak akses dengan mengubah request frontend.
Setiap operasi penyelenggara harus memeriksa `organizationId` dari identitas terautentikasi dan data acara.
14.3 Firestore Security Rules
Rules harus menerapkan prinsip least privilege.
Ketentuan minimum:
Mahasiswa hanya dapat membaca dan mengubah data profil yang diizinkan.
Mahasiswa hanya dapat membaca tiket dan registrasi miliknya.
Penyelenggara hanya dapat membaca dan mengelola data organisasi sendiri.
Admin memiliki akses sesuai peran.
Field sensitif dan penghitung kuota tidak dapat diubah langsung oleh klien.
Data token tiket tidak boleh dapat dibaca secara bebas.
Audit log tidak dapat diubah oleh pengguna biasa.
14.4 Validasi Backend
Semua proses berikut wajib divalidasi ulang di backend:
Pendaftaran acara.
Pembatalan pendaftaran.
Penerbitan dan verifikasi tiket.
Check-in.
Perubahan kehadiran.
Persetujuan acara.
Perubahan acara.
Ekspor peserta.
Penetapan role.
14.5 Perlindungan Data
Kumpulkan hanya data yang diperlukan.
Jangan menampilkan NBI atau data pribadi sensitif pada QR Code.
Hindari menyimpan password, token mentah, atau kredensial dalam log.
Gunakan HTTPS untuk komunikasi.
Batasi masa berlaku URL file sementara.
Terapkan validasi tipe dan ukuran file untuk poster yang diunggah.
---
15. Integrasi dan Konfigurasi
15.1 Firebase
Proyek Firebase perlu mengaktifkan layanan yang digunakan:
Firebase Authentication.
Cloud Firestore.
Cloud Functions.
Firebase Storage.
Google Sign-In harus dikonfigurasi pada Firebase Authentication.
15.2 Environment Variables
Konfigurasi frontend menggunakan environment variables Vite.
Contoh `.env.example`:
```env
VITE_FIREBASE_API_KEY=
VITE_FIREBASE_AUTH_DOMAIN=
VITE_FIREBASE_PROJECT_ID=
VITE_FIREBASE_STORAGE_BUCKET=
VITE_FIREBASE_MESSAGING_SENDER_ID=
VITE_FIREBASE_APP_ID=
```
File `.env` yang berisi konfigurasi proyek lokal tidak boleh di-commit apabila berisi nilai yang tidak dimaksudkan untuk dibagikan. Gunakan `.env.example` sebagai template.
Firebase client configuration bukan pengganti aturan keamanan. Perlindungan data tetap harus dilakukan melalui Authentication, Security Rules, dan Cloud Functions.
15.3 Integrasi SIMPOINT
MVP hanya menampilkan informasi SKPI yang disimpan pada data acara.
Detail acara dapat menyediakan tautan eksternal menuju SIMPOINT.
Sinkronisasi otomatis melalui API tidak termasuk MVP.
Jangan mengklaim poin telah tersinkron otomatis jika proses tersebut belum diimplementasikan dan diverifikasi.
15.4 Ekspor CSV
Ekspor peserta dilakukan melalui Cloud Function agar hak akses dapat diperiksa di backend. File ekspor hanya memuat data yang relevan untuk operasional acara.
---
16. Pengujian
16.1 Pengujian Fungsional
Area	Skenario
Login	Login dengan email/password valid
Login	Login dengan NBI/password valid
Login	NBI dengan jumlah digit tidak sesuai
Login	Password salah
Google Sign-In	Login dengan akun Google
Katalog	Menampilkan daftar acara
Filter	Filter kategori, bulan, dan SKPI
Detail	Menampilkan detail acara dengan benar
Pendaftaran	Pendaftaran berhasil
Pendaftaran	Pendaftaran duplikat ditolak
Kuota	Pendaftaran saat kuota penuh ditolak
Sesi	Pendaftaran sesi yang tersedia berhasil
Tiket	Tiket dan QR dibuat setelah pendaftaran berhasil
Check-in	QR valid berhasil digunakan satu kali
Check-in	QR yang sudah digunakan ditolak
Pembatalan	Pembatalan dalam batas waktu berhasil
Pembatalan	Pembatalan kurang dari 24 jam sebelum acara ditolak
Organizer	Data organisasi lain tidak dapat diakses
Admin	Persetujuan acara berfungsi
Ekspor	CSV hanya memuat data dalam cakupan akses
16.2 Pengujian Keamanan
Pengguna tanpa login tidak dapat mengakses halaman privat.
Mahasiswa tidak dapat mengakses route admin atau penyelenggara.
Penyelenggara tidak dapat mengakses data organisasi lain.
Pengguna tidak dapat mengubah role sendiri.
Request langsung ke Cloud Functions tetap menjalankan validasi.
Token QR tidak dapat digunakan ulang.
Data sensitif tidak terekspos melalui response atau log.
Penghitung kuota tidak dapat dimanipulasi dari frontend.
16.3 Pengujian UI/UX
Seluruh delapan frame utama memiliki implementasi yang sesuai.
Layout responsif.
Form memiliki validasi dan pesan kesalahan.
Loading, Empty State, dan Error State tersedia.
Kontras dan keterbacaan teks memadai.
Navigasi konsisten.
Komponen tidak menggunakan dekorasi berlebihan yang mengganggu fungsi.
---
17. Deployment
17.1 Version Control
Source code disimpan di GitHub.
Perubahan dikerjakan melalui branch fitur jika memungkinkan.
Perubahan penting ditinjau sebelum digabungkan ke branch utama.
File konfigurasi rahasia tidak boleh di-commit.
17.2 Frontend Deployment
Frontend dibangun menggunakan Vercel.
Repository GitHub dihubungkan ke proyek Vercel.
Environment variables Firebase diatur melalui konfigurasi proyek Vercel.
Setiap perubahan pada branch yang terhubung dapat menghasilkan deployment preview.
Branch produksi digunakan untuk deployment final.
17.3 Firebase Deployment
Firestore Security Rules dan indexes harus disiapkan.
Cloud Functions harus di-deploy ke proyek Firebase yang benar.
Firebase Authentication harus memiliki provider yang diperlukan.
Storage Rules harus membatasi akses unggah dan baca file.
Pengujian dilakukan pada environment pengembangan sebelum rilis.
---
18. Definition of Done
Implementasi MVP dapat dinyatakan selesai apabila:
[ ] Pengguna dapat login melalui metode autentikasi yang disepakati.
[ ] Login NBI menggunakan resolver server yang aman dan tidak hanya mengandalkan pencarian data di frontend.
[ ] Profil dan role pengguna dimuat dengan benar.
[ ] Mahasiswa dapat melihat beranda dan katalog.
[ ] Filter katalog bekerja.
[ ] Detail acara menampilkan informasi yang diperlukan, termasuk informasi SKPI jika tersedia.
[ ] Mahasiswa dapat mendaftar acara yang memenuhi syarat.
[ ] Validasi kuota dan pendaftaran duplikat berjalan di backend.
[ ] Pilihan sesi dan kuota sesi bekerja untuk acara yang menggunakan sesi.
[ ] Tiket elektronik dan QR token unik dibuat setelah pendaftaran berhasil.
[ ] Tiket dapat dilihat kembali dan diunduh.
[ ] Pembatalan mematuhi batas 24 jam dan mengembalikan kuota tepat satu kali.
[ ] Check-in QR hanya dapat dilakukan satu kali.
[ ] Pencatatan kehadiran manual memiliki alasan dan audit log.
[ ] Penyelenggara hanya dapat mengakses data organisasinya.
[ ] Statistik penyelenggara hanya mencakup kegiatan organisasinya.
[ ] Admin dapat mengelola pengguna, organisasi, dan persetujuan acara.
[ ] Ekspor CSV memeriksa otorisasi di backend.
[ ] Security Rules dan Cloud Functions telah diuji.
[ ] Delapan frame utama Figma telah diimplementasikan secara responsif.
[ ] Loading, Empty State, dan Error State tersedia.
[ ] Aplikasi berhasil di-deploy dan dapat diakses melalui URL deployment.
---
19. Asumsi dan Batasan
Produk dikembangkan sebagai aplikasi web.
MVP menggunakan Firebase sebagai backend service.
Frontend menggunakan React.js, React Router, dan Tailwind CSS.
Hosting frontend menggunakan Vercel.
Pendaftaran pada MVP tidak memerlukan pembayaran.
Zona waktu operasional aplikasi adalah `Asia/Jakarta`.
Data NBI harus berasal dari sumber yang sah atau proses verifikasi yang ditentukan tim/kampus.
Jika sumber data NBI resmi belum tersedia, implementasi login NBI memerlukan pemetaan akun yang telah diverifikasi dan dikelola secara aman.
Integrasi otomatis SIMPOINT tidak termasuk MVP.
Fitur dashboard penyelenggara dan admin merupakan kebutuhan fungsional tambahan di luar delapan frame utama Figma.
Ketersediaan fitur Firebase dapat bergantung pada konfigurasi dan paket layanan proyek.
---
20. Pengembangan Berikutnya
Setelah MVP stabil, pengembangan dapat mempertimbangkan:
Integrasi resmi dengan SIMPOINT jika API dan izin akses tersedia.
Notifikasi email atau WhatsApp.
Pembayaran untuk acara berbayar.
Sinkronisasi kalender.
Rekomendasi kegiatan berdasarkan minat.
Analitik penyelenggara yang lebih lengkap.
Peningkatan aksesibilitas dan dukungan multi-bahasa.
Aplikasi mobile native jika kebutuhan pengguna telah tervalidasi.
Pengembangan lanjutan harus diprioritaskan berdasarkan kebutuhan nyata pengguna dan kesiapan integrasi, bukan sekadar menambah jumlah fitur.
---
21. Referensi Desain
21.1 Figma Design
UNTAG Event Hub — UI/UX Design
21.2 Figma Prototype
UNTAG Event Hub — Prototype
---
Akhir Dokumen — PRD UNTAG Event Hub
