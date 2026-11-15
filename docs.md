# UII Application Support

## Ringkasan Ide Produk --- Versi Terbaru

**Status:** Konsep dan prototype MVP\
**Target:** Demo internal / hackathon\
**Platform:** Web application, siap dipublikasikan melalui Vercel\
**Pendekatan prototype:** Frontend-first dengan data simulasi dan
`localStorage`

------------------------------------------------------------------------

## 1. Ringkasan Produk

**UII Application Support** adalah platform terpusat untuk melaporkan,
mengelola, mendistribusikan, dan memantau kendala pada berbagai aplikasi
internal Universitas Islam Indonesia (UII).

Platform menyediakan dua jalur pelaporan:

1.  **Embedded Report Issue** --- tombol laporan yang dapat dipasang di
    dalam aplikasi internal. Informasi aplikasi dan halaman asal
    diteruskan ke form laporan.
2.  **Standalone Dashboard** --- pengguna masuk langsung ke UII
    Application Support dan membuat laporan melalui dashboard. Jika
    tidak ada konteks aplikasi, pengguna memilih aplikasi asal secara
    manual.

Semua laporan masuk ke satu sistem ticket management agar pengguna,
developer, dan administrator dapat memantau proses penanganan melalui
satu tempat.

> Untuk prototype, integrasi UII SSO dan aplikasi internal
> disimulasikan. Jangan menyatakan integrasi production sudah tersedia.

## 2. Masalah yang Ingin Diselesaikan

-   Laporan gangguan aplikasi tersebar melalui berbagai kanal.
-   Informasi laporan sering tidak seragam atau kurang lengkap.
-   Distribusi laporan kepada tim developer berpotensi dilakukan secara
    manual.
-   Pengguna kesulitan mengetahui siapa yang menangani dan sejauh mana
    progres laporan.
-   Riwayat komunikasi dan penyelesaian masalah belum terpusat.

## 3. Solusi yang Ditawarkan

Satu platform layanan dukungan aplikasi yang menyediakan: - Form
pelaporan terstruktur. - Identifikasi aplikasi asal laporan. - Nomor
tiket otomatis. - Penentuan tim dan developer melalui automatic
assignment. - Dashboard berbeda berdasarkan role. - Status dan timeline
penanganan tiket. - Komunikasi antara pelapor dan developer. -
Monitoring dan pengelolaan oleh administrator. - Riwayat aktivitas untuk
pelacakan dan audit.

## 4. Pengguna dan Hak Akses

### User / Pelapor

-   Login melalui simulasi UII SSO.
-   Membuat laporan kendala.
-   Melihat daftar dan detail tiket miliknya.
-   Mengirim komentar atau informasi tambahan.
-   Memantau status dan riwayat tiket.
-   Mengonfirmasi penyelesaian atau membuka kembali tiket jika masalah
    belum selesai.

### Developer

-   Melihat tiket yang ditugaskan kepadanya.
-   Melihat detail masalah dan aplikasi asal.
-   Mengubah status penanganan.
-   Menambahkan komentar publik.
-   Menambahkan catatan internal yang hanya dapat dilihat pihak
    berwenang.
-   Menandai tiket sebagai selesai.

### Administrator

-   Melihat seluruh tiket.
-   Memantau statistik dan distribusi tiket.
-   Mengelola data aplikasi, tim, developer, dan kategori.
-   Mengelola routing rules.
-   Memantau tiket yang belum mendapatkan assignment.
-   Melihat audit log dan aktivitas sistem.

## 5. Alur Utama Sistem

1.  Pengguna membuka aplikasi internal atau UII Application Support.
2.  Pengguna menekan **Report Issue** atau membuka menu **Buat
    Laporan**.
3.  Sistem menampilkan form laporan.
4.  Jika laporan berasal dari embedded integration, aplikasi dan halaman
    asal diisi otomatis berdasarkan konteks yang diteruskan.
5.  Pengguna mengisi judul, kategori, prioritas, deskripsi, dan lampiran
    opsional.
6.  Sistem membuat nomor tiket, misalnya `UII-2026-0001`.
7.  Sistem menjalankan automatic assignment berdasarkan routing rules.
8.  Tiket diberikan kepada tim dan developer yang sesuai.
9.  Developer memeriksa laporan, berkomunikasi dengan pelapor, dan
    memperbarui status.
10. Pengguna memantau progres melalui halaman detail tiket.
11. Setelah masalah selesai, developer mengubah status menjadi
    **RESOLVED**.
12. Pengguna dapat mengonfirmasi penyelesaian atau melakukan
    **REOPENED** jika masalah belum selesai.

## 6. Automatic Ticket Assignment

Assignment prototype menggunakan aturan sederhana dan deterministik:

1.  Cocokkan aplikasi asal dan kategori dengan routing rules.
2.  Tentukan tim tujuan.
3.  Pilih developer aktif dalam tim tersebut.
4.  Prioritaskan developer dengan jumlah tiket aktif paling sedikit.
5.  Jika jumlahnya sama, gunakan urutan pemilihan yang konsisten.
6.  Jika tidak ada aturan atau developer tersedia, masukkan tiket ke
    **Unassigned Queue** untuk ditangani administrator.

Contoh routing:

  Aplikasi / Kategori         Tim Tujuan
  --------------------------- -------------------------
  Academic Gateway            Academic Development
  Examination                 Examination Development
  Lecture / UI                Frontend Team
  Service / Gangguan Sistem   Backend Team
  Login / Akses               Infrastructure Team

Routing rules dapat dikelola oleh administrator.

## 7. Status dan Siklus Tiket

-   `OPEN` --- laporan baru dibuat.
-   `ASSIGNED` --- tiket telah ditugaskan.
-   `IN PROGRESS` --- sedang dikerjakan developer.
-   `WAITING FOR USER` --- menunggu informasi dari pelapor.
-   `RESOLVED` --- developer menyatakan masalah selesai.
-   `CLOSED` --- tiket ditutup.
-   `REOPENED` --- tiket dibuka kembali karena masalah belum
    terselesaikan.

Setiap perubahan status harus memperbarui data tiket dan dicatat dalam
timeline aktivitas.

## 8. Fitur MVP Prototype

### Prioritas wajib

-   Login demo dan pemilihan role.
-   User dashboard.
-   Form buat laporan.
-   Daftar dan detail tiket.
-   Automatic assignment sederhana.
-   Developer dashboard dan daftar tiket.
-   Update status dan komentar.
-   Admin dashboard dan tampilan seluruh tiket.
-   Penyimpanan data demo menggunakan `localStorage`.
-   Tampilan responsive.
-   Production build yang berhasil.

### Fitur tambahan jika waktu mencukupi

-   Embedded Report Issue pada halaman simulasi aplikasi Examination.
-   Routing Rules Management.
-   Notification Center.
-   Audit Log.
-   Grafik statistik sederhana.
-   Upload lampiran dengan validasi dasar.

### Di luar cakupan prototype cepat

-   Integrasi UII SSO sebenarnya.
-   Integrasi backend dan database internal UII.
-   Integrasi production ke seluruh aplikasi internal.
-   Email atau notifikasi real-time.
-   Engine assignment kompleks.
-   SLA dan analytics lanjutan.

## 9. Teknologi Prototype

Rekomendasi implementasi cepat: - **Framework:** Next.js + React +
TypeScript. - **Styling:** Tailwind CSS. - **UI:** shadcn/ui atau
komponen reusable sejenis. - **Icons:** Lucide React. - **Penyimpanan
demo:** `localStorage`. - **Deployment:** Vercel.

Teknologi dapat disesuaikan dengan project yang sudah tersedia. Untuk
mengejar demo, hindari layanan eksternal yang membutuhkan setup panjang.

Gunakan data dummy yang realistis. Prototype harus tetap dapat dibuka
tanpa konfigurasi backend atau environment variable eksternal.

## 10. Arah Desain UI/UX

Gaya visual: - Professional enterprise dashboard. - Modern, clean,
minimal, dan mudah dipahami. - Terinspirasi dari sistem informasi
institusi pendidikan. - Sidebar navy, konten berlatar putih atau light
gray. - Card sederhana, tabel rapi, status badge jelas. - Responsive
untuk desktop, tablet, dan mobile. - Bahasa antarmuka: Indonesia.

Palet warna acuan:

  Elemen           Warna
  ---------------- -----------
  Primary Navy     `#142B4A`
  Primary Blue     `#2563EB`
  Light Blue       `#EFF6FF`
  Background       `#F8FAFC`
  Surface          `#FFFFFF`
  Border           `#E2E8F0`
  Text Primary     `#1E293B`
  Text Secondary   `#64748B`

## 11. Data dan Entitas Konseptual

Entitas yang disiapkan untuk pengembangan lebih lanjut: - `users` -
`applications` - `teams` - `team_members` - `categories` -
`routing_rules` - `tickets` - `ticket_assignments` - `ticket_comments` -
`ticket_attachments` - `ticket_status_histories` - `notifications` -
`audit_logs`

Prototype cepat boleh menyimpan struktur tersebut dalam repository
mock/localStorage. Untuk production, pindahkan ke backend dan database
relational dengan kontrol akses server-side.

## 12. Keamanan dan Governance

Ketika beralih ke production: - Verifikasi identitas melalui UII SSO di
sisi server. - Terapkan Role-Based Access Control (RBAC). - Jangan
mempercayai `user_id`, role, atau source application hanya dari
browser/query parameter. - Validasi sumber aplikasi melalui mekanisme
integrasi yang disetujui. - Pisahkan komentar publik dan catatan
internal. - Validasi tipe, ukuran, dan isi file lampiran. - Simpan audit
trail untuk aktivitas penting. - Batasi akses tiket sesuai role dan
kewenangan. - Jangan menaruh secret atau service-role key di frontend. -
Terapkan HTTPS dan kebijakan penyimpanan data sesuai ketentuan UII.

## 13. Skenario Demo End-to-End

**Skenario 1 --- User membuat tiket** - Login sebagai User. - Buat
laporan untuk aplikasi Examination. - Isi kategori Bug / Error dan
deskripsi masalah. - Submit laporan. - Tunjukkan nomor tiket dan hasil
automatic assignment.

**Skenario 2 --- Developer menangani tiket** - Login sebagai Developer
yang menerima tiket. - Buka tiket yang ditugaskan. - Ubah status menjadi
`IN PROGRESS`. - Tambahkan komentar. - Ubah status menjadi `RESOLVED`.

**Skenario 3 --- User memantau hasil** - Login kembali sebagai User. -
Buka tiket yang dibuat. - Tunjukkan status terbaru, komentar, dan
timeline penyelesaian.

**Skenario 4 --- Admin memantau sistem** - Login sebagai
Administrator. - Tampilkan seluruh tiket. - Periksa distribusi tiket dan
workload developer. - Tunjukkan routing rules atau Unassigned Queue jika
tersedia.

**Skenario 5 --- Embedded Report Issue** - Buka halaman simulasi
Examination. - Klik tombol Report Issue. - Tunjukkan bahwa aplikasi asal
otomatis terisi. - Kirim laporan dan buktikan tiket masuk ke daftar
tiket yang sama.

## 14. Batasan Prototype dan Rencana Lanjutan

Prototype membuktikan alur produk dan interaksi utama, bukan kesiapan
production.

  -----------------------------------------------------------------------
  Area                    Prototype               Pengembangan production
  ----------------------- ----------------------- -----------------------
  Login                   Demo role selector      Integrasi UII SSO

  Data                    localStorage / mock     Backend dan database
                          repository              resmi

  Embedded report         Simulasi context        Integrasi dan validasi
                          aplikasi                server-side

  Assignment              Routing rules sederhana Aturan operasional dan
                                                  workload aktual

  Notification            In-app simulasi         Notification service

  Security                Pembatasan demo         RBAC dan kontrol
                                                  server-side

  Deployment              Vercel                  Infrastruktur sesuai
                                                  kebijakan UII
  -----------------------------------------------------------------------

## 15. Indikator Keberhasilan Demo

Prototype dianggap berhasil jika: - Ketiga role dapat dicoba. - User
dapat membuat tiket. - Nomor tiket terbentuk otomatis. - Aplikasi asal
tercatat. - Assignment menghasilkan tim dan developer. - Developer dapat
memperbarui status dan memberi komentar. - User dapat melihat perubahan
status dan timeline. - Admin dapat melihat seluruh tiket. - Data demo
bertahan setelah refresh pada browser yang sama. - Aplikasi berhasil
di-build dan dapat diakses melalui Vercel.

## Ringkasan Satu Kalimat

**UII Application Support adalah platform ticketing terpusat yang
menghubungkan pengguna aplikasi internal UII dengan tim developer
melalui pelaporan terstruktur, automatic ticket assignment, dan
pemantauan penyelesaian masalah secara transparan.**