# PRODUCT REQUIREMENTS DOCUMENT (PRD)
## Prototype Website Angkatan Muda Airlow

**Versi:** 1.1 — Penyelarasan persetujuan dan penerbitan  
**Tanggal:** 24 Oktober 2026  
**Status:** Perencanaan; belum diimplementasikan  
**Pemilik proyek:** Kelompok pengembang prototype Angkatan Muda Airlow  
**Catatan identitas:** Nama kerja, logo placeholder, dan seluruh konten organisasi adalah simulasi; tidak mewakili identitas resmi organisasi.

## 1. Ringkasan eksekutif
Proyek ini bertujuan merancang dan kemudian membangun prototype fungsional website Angkatan Muda Airlow dengan dua area: website publik untuk informasi organisasi dan dashboard internal untuk pengelolaan konten serta data anggota simulasi. Pengembangan dimulai secara lokal dan dapat di-hosting hanya untuk demonstrasi setelah pengujian. Prototype bukan website resmi organisasi dan tidak akan menggunakan data pribadi anggota sebenarnya.

Visi produk: pengalaman yang modern dan energik namun bersih, mudah dinavigasi di ponsel, dapat dikelola pengurus nonteknis, dan memiliki dasar kode serta keamanan yang layak dikembangkan lebih lanjut.

## 2. Tujuan, hasil, dan batasan
### 2.1 Tujuan
- Menyediakan beranda publik yang cepat menunjukkan kegiatan terdekat, pengumuman penting, dan berita terkini.
- Menyajikan profil, struktur kepengurusan, bidang pelayanan, program kerja, kalender kegiatan, berita, galeri, dan kontak.
- Memungkinkan Admin dan Pengurus mengelola konten melalui dashboard dengan pembatasan akses.
- Menyediakan alur persetujuan konten sebelum informasi Pengurus dipublikasikan.
- Memberikan media pembelajaran full-stack yang dapat diuji dan didemonstrasikan menggunakan data simulasi.

### 2.2 Di luar cakupan MVP
- Situs resmi organisasi, penggunaan logo resmi tanpa izin, domain resmi, dan publikasi data produksi.
- Registrasi akun secara publik, pembayaran online, absensi kegiatan, pendaftaran peserta, dan aplikasi native Android/iOS.
- Integrasi WhatsApp otomatis, streaming/video hosting internal, serta pustaka media lengkap dengan penggunaan ulang lintas konten.
- Sistem administrasi keuangan dan dokumen keanggotaan sensitif.

### 2.3 Asumsi dan hal yang perlu konfirmasi kemudian
- Struktur kelompok/sektor dan nama bidang organisasi masih menggunakan data contoh.
- Nama organisasi, logo, warna, sejarah, visi-misi, dan kontak resmi akan dikonfirmasi sebelum ada penggunaan nyata.
- Penyedia hosting, domain, dan skenario produksi belum dipilih.
- Skema data anggota final disepakati setelah validasi kebutuhan pengurus yang sebenarnya.

## 3. Pengguna dan peran
### 3.1 Pengunjung publik
Tanpa login, dapat membaca informasi publik, mencari/menyaring kegiatan, melihat galeri dan berita, serta mengakses kontak. Tidak dapat melihat daftar anggota internal atau dashboard.

### 3.2 Pengurus
Login menggunakan akun buatan Admin. Dapat menyusun/memperbarui draft konten dan mengajukannya untuk persetujuan; melihat status dan catatan revisi; melihat daftar anggota terbatas pada nama, kelompok, dan status. Tidak dapat mengimpor/mengekspor anggota, melihat atribut privat lain, mengelola akun Admin, atau menerbitkan konten sendiri.

### 3.3 Admin
Mengelola akun internal, seluruh konten, persetujuan, konfigurasi dasar, dan data anggota simulasi, termasuk input manual dan impor/ekspor. Memiliki audit log dan kemampuan meninjau proses publikasi. Aksi penting dicatat.

## 4. Arsitektur informasi dan navigasi
### 4.1 Halaman publik — pendekatan hybrid
- `/` — beranda ringkas: identitas, jadwal terdekat, pengumuman, berita terbaru, dan navigasi jelas.
- `/tentang` — sejarah singkat, visi, misi, dan bidang pelayanan.
- `/pengurus` — struktur pengurus, jabatan, dan masa bakti dari data simulasi.
- `/program-kerja` dan `/program-kerja/{slug}` — daftar program kerja dan detail.
- `/kegiatan` — daftar agenda dan kalender bulanan; `/kegiatan/{slug}` untuk detail.
- `/berita` dan `/berita/{slug}` — daftar dan detail berita.
- `/pengumuman` dan `/pengumuman/{slug}` — pengumuman dan detail.
- `/galeri` dan `/galeri/{slug}` — album kegiatan dan foto.
- `/kontak` — kontak contoh dan informasi bahwa situs masih simulasi.

Rute di atas adalah usulan awal dan boleh berubah pada desain teknis. Beranda bukan satu halaman yang memuat semua isi; halaman detail tetap sederhana dan mudah ditemukan.

### 4.2 Dashboard internal
- `/login` — autentikasi internal; tidak ada tombol pendaftaran publik.
- `/dashboard` — ringkasan pekerjaan, jadwal, dan status konten.
- `/dashboard/kegiatan`, `/dashboard/berita`, `/dashboard/pengumuman`, `/dashboard/galeri` — pengelolaan sesuai izin.
- `/dashboard/persetujuan` — antrian review khusus Admin.
- `/dashboard/anggota` — daftar terbatas untuk Pengurus; pengelolaan lengkap khusus Admin.
- `/dashboard/pengguna`, `/dashboard/pengaturan`, `/dashboard/organisasi` — fungsi khusus Admin; organisasi mencakup profil, bidang, masa bakti, kepengurusan, program kerja, dan kontak.
- `/dashboard/audit-log` — antarmuka audit khusus Admin pada fase lanjutan. Logging minimum aksi penting tersedia sejak MVP.

## 5. Kebutuhan fungsional dan prioritas
### 5.1 MVP (harus berfungsi dalam demo awal)
**FR-01 Beranda dan navigasi:** Informasi penting muncul lebih dahulu; navigasi mobile dapat dibuka, ditutup, dioperasikan keyboard, dan menunjukkan halaman aktif.

**FR-02 Profil dan organisasi:** Halaman publik berisi data simulasi sejarah, visi-misi, struktur pengurus, masa bakti, bidang, program kerja, dan kontak. Hanya Admin menyunting modul organisasi pada MVP; Pengurus membaca versi publik. Simpan perubahan sebagai revisi paket organisasi, setujui, lalu terbitkan melalui aksi terpisah; versi publik lama tidak berubah saat draft disunting.

**FR-03 Kegiatan dan kalender:** Admin/Pengurus membuat draft kegiatan (judul, jenis, tanggal/waktu lokal, tempat, deskripsi, status). Pengunjung dapat beralih antara daftar mendatang dan kalender bulanan, membuka detail, dan melihat keadaan kosong yang jelas.

**FR-04 Berita dan pengumuman:** CRUD draft, unggah foto utama opsional, preview, pengajuan review, serta halaman publik hanya untuk konten berstatus terbit.

**FR-05 Alur persetujuan:** Simpan draft → ajukan → Admin menyetujui/meminta revisi/menolak → bila disetujui, Admin menerbitkan melalui aksi terpisah. Persetujuan tidak membuka akses publik. Setiap perubahan isi konten terbit, termasuk oleh Admin, menghasilkan revisi baru yang memerlukan persetujuan ulang dan penerbitan terpisah. Versi publik lama tetap tampil sampai revisi pengganti diterbitkan. Pengurus tidak dapat melompati proses melalui URL/API/action Livewire.

**FR-06 Autentikasi dan peran:** Login/logout, pembatasan login, dua peran, akun dibuat Admin saja, kebijakan akses di backend, halaman 403 yang informatif. Tidak ada registrasi publik.

**FR-07 Pendataan anggota sederhana:** Admin melakukan CRUD anggota simulasi dan pencarian/paginasi; Pengurus hanya memperoleh nama, kelompok, status. Daftar internal tidak memiliki rute publik dan tidak mengekspos field privat dalam respons aplikasi untuk Pengurus.

**FR-08 Media foto:** Unggah file gambar yang tervalidasi, kompresi serta thumbnail, alt text, kaitkan foto ke kegiatan/album; hak akses upload dan penghapusan dicek di server. Media disetujui belum otomatis publik. File asli dan seluruh turunannya hanya dapat diakses publik bila dipakai versi konten/album/organisasi yang sedang diterbitkan dan media tersebut disetujui. Preview privat memerlukan autentikasi dan otorisasi; menebak URL tidak memberi akses.

**FR-09 Dashboard:** Ringkasan jumlah draft, konten menunggu persetujuan, revisi disetujui tetapi belum diterbitkan, kegiatan mendatang, dan aksi sesuai peran. Status versi publik dan revisi terbaru ditampilkan terpisah. UI sederhana untuk pengurus nonteknis.

**FR-10 Konten simulasi dan indikator prototype:** Seeder membuat contoh organisasi, kegiatan, berita, dan anggota fiktif. Penanda “Prototype / data simulasi” jelas pada antarmuka demonstrasi, bukan mengaku sebagai website resmi.

### 5.2 Lanjutan setelah MVP stabil
**FR-11 Impor/ekspor Excel/CSV:** Hanya Admin; pemetaan kolom, validasi baris, pratinjau hasil, penanganan duplikat, laporan error, serta pembatasan ukuran file. Ekspor hanya field yang diizinkan.

**FR-12 Audit log:** Catat aktor, tindakan, target, waktu, serta ringkasan perubahan penting tanpa menyimpan password/token/data sensitif ke log.

**FR-13 Backup/pemulihan:** Cadangan berkala sesuai lingkungan, penyimpanan aman, dan prosedur pemulihan yang diuji.

**FR-14 Penyempurnaan galeri:** Pengaturan urutan foto, pengelompokan album yang lebih kaya, penghapusan aman ketika gambar dipakai pada konten lain.

**FR-15 Pengujian dan hardening tambahan:** Otomasi skenario browser, pengecekan screen reader, optimasi gambar/performa, dan verifikasi hosting demo.

Catatan: FR-11–FR-13 tetap merupakan kebutuhan keamanan dan pengelolaan yang telah dipilih. Penempatan pada fase lanjutan tidak mengizinkan demo publik memakai data nyata sebelum kontrol yang relevan tersedia.

## 6. Alur persetujuan konten
### 6.1 Kamus status bersama
Kamus ini digunakan identik oleh ERD, Design System, dan Wireframe. Status revisi berbeda dari status publikasi parent; status anggota/program/impor adalah domain lain.

| Lingkup | Nilai | Label UI |
|---|---|---|
| Revisi | `draft` | Draft |
| Revisi | `pending_review` | Menunggu persetujuan |
| Revisi | `revision_requested` | Perlu revisi |
| Revisi | `approved` | Disetujui |
| Revisi | `rejected` | Ditolak |
| Publikasi | `unpublished` | Belum terbit |
| Publikasi | `published` | Terbit |
| Publikasi | `archived` | Arsip |

Revisi yang pernah diterbitkan tetapi bukan versi aktif diberi keterangan **Versi terdahulu** atau **Diarsipkan** sesuai riwayat; jangan menyebutnya belum diterbitkan. Keterangan ini bukan status revisi baru.

Untuk revisi approved yang belum pernah diterbitkan, tampilkan bantuan **Disetujui — belum diterbitkan**. Moderasi media memakai `pending_review`, `approved`, `rejected`; keterbitan media diturunkan dari pemakaian pada publikasi aktif, bukan status approved saja.

### 6.2 Transisi dan aktor
1. Pengurus membuat/mengedit draft kegiatan atau post miliknya/yang ditugaskan; Admin mengelola semua. Profil organisasi dan album tetap Admin-only pada MVP.
2. `draft → pending_review`: penulis berizin mengajukan versi tertentu. Setelah diajukan, isi, lampiran, dan metadata publik revisi dibekukan; transisi status tetap diizinkan oleh operasi resmi.
3. `pending_review → approved / revision_requested / rejected`: hanya Admin; alasan wajib untuk dua keputusan terakhir. Satu keputusan final per versi. Pengajuan ulang membuat versi draft baru, tidak menimpa keputusan lama.
4. **Setujui** hanya mencatat keputusan, reviewer, dan waktu; tidak mengubah versi publik, status publikasi, atau waktu penerbitan.
5. **Terbitkan** hanya oleh Admin untuk revisi approved yang masih berlaku, setelah memeriksa media dan target versi. Operasi terpisah ini mengganti penunjuk versi publik dan mencatat penerbit/waktu secara atomik. Tidak ada publikasi otomatis atau terjadwal dalam MVP.
6. Revisi baru atas konten published tidak mengubah versi publik sebelumnya, termasuk sesudah revisi baru approved. Hanya penerbitan pengganti yang mengubah tampilan publik. Admin juga mengikuti alur tersebut; Admin boleh menyetujui karyanya sendiri melalui aksi eksplisit, tanpa memalsukan reviewer lain. Tidak diwajibkan dua orang Admin berbeda.
7. Admin dapat menarik terbit dengan mengarsipkan (`published → archived`); publik tidak lagi mengakses konten. Penerbitan kembali memerlukan aksi Terbitkan dan validasi ulang atas revisi approved yang dipilih. Riwayat tetap disimpan; alasan arsip dicatat.

### 6.3 Identitas URL, waktu, dan kepemilikan
- Slug huruf kecil, angka, dan tanda hubung; maksimal 190 karakter. Slug unik pada masing-masing events, posts (bersama news/announcement), gallery_albums, dan programs. Benturan diberi akhiran angka secara atomik; slug kosong memakai prefiks jenis dan pengenal stabil.
- Slug dapat disunting Admin sebelum penerbitan pertama, kemudian tetap meski judul berubah. MVP tidak menyediakan penggantian slug pascaterbit; kebutuhan penggantian kelak memerlukan redirect permanen. Slug soft-deleted tetap dicadangkan. Tipe post tetap setelah terbit.
- `created_by` adalah pembuat awal yang tidak berubah; `owner_id` adalah penanggung jawab kegiatan/post, `assigned_editor_id` opsional adalah satu penyunting tambahan pada MVP, dan `author_id` adalah penulis setiap revisi. Hanya Admin mengubah pemilik/penugasan; perubahan tidak memberi hak menyetujui atau menerbitkan kepada Pengurus.
- Waktu disimpan UTC, ditampilkan WIT (`Asia/Jayapura`) untuk demo. Catat pengajuan, keputusan, dan penerbitan secara berbeda. `published_at` menunjukkan waktu publikasi aktif; riwayat menyimpan setiap penerbitan versi. UI dapat membedakan Terbit pertama dan Diperbarui berdasarkan riwayat; jangan memakai updated_at sebagai tanggal terbit.
- Pengumuman penting ditandai pada revisi yang disetujui; sampul album dipilih dari foto disetujui dalam versi album yang diterbitkan. Pengubahan keduanya mengikuti review/penerbitan ulang.

## 7. Data dan rancangan entitas awal
Rancangan konseptual (bukan migration final):
- `roles`, `users`: akun internal, role_id, is_active, email unik, password hash pada kolom password, timestamps.
- `members`: id, name, gender opsional, group_id, membership_status, joined_at opsional, timestamps. Gunakan data fiktif.
- `groups`: id, name, description opsional.
- `organization_profiles`: sejarah, visi, misi, kontak simulasi dan identitas visual sementara.
- `terms`, `leaderships`: masa bakti, jabatan, nama tampilan simulasi, urutan (padanan konseptual leadership_terms/leadership_positions v1.0).
- `service_fields`, `programs`: bidang pelayanan serta program kerja (work_programs v1.0).
- `events`, `event_revisions`, `posts`, `post_revisions`: identitas/slug/pemilik terpisah dari isi versi dan status revisi; post bertipe news/announcement.
- `media_files`, `media_variants`, `gallery_albums`, `album_media`, `media_reviews`: file privat, optimasi, draft album dan moderasi foto; gallery_albums adalah padanan albums v1.0.
- `managed_content_revisions`: snapshot versi paket organisasi atau album Admin-only; versi publik tetap terpisah dari tabel kerja.
- `revision_media`: referensi media dan metadata tampilan per revisi yang dibekukan.
- `review_decisions`, `publication_actions`: keputusan persetujuan dan riwayat penerbitan/arsip terpisah (penajaman content_reviews v1.0).
- `audit_logs`: aktor, aksi, model, id target, waktu, metadata aman.

Gunakan foreign key, indeks pencarian/status/tanggal, unique pada slug dalam ruang yang tepat, validasi kolom wajib, dan penghapusan yang tidak meninggalkan referensi rusak. ERD v1.1 menetapkan target revisi dengan FK eksplisit dan constraint tepat satu target, bukan polimorfik tanpa FK. Tabel pendukung versi/publikasi merupakan pengamanan fitur MVP yang sudah dipilih, bukan fitur produk tambahan.

## 8. Aturan bisnis dan keamanan
- Larang registrasi publik; Admin membuat akun Pengurus secara terkontrol.
- Password di-hash memakai mekanisme Laravel yang didukung; simpan secret di `.env`, tidak ke repository.
- Semua route/action/query internal memakai autentikasi dan otorisasi server-side (Policies/Gates), tidak sekadar menyembunyikan tombol.
- Role Pengurus hanya menerima field nama/kelompok/status anggota; kebijakan sama diterapkan pada pencarian, respons Livewire, API, ekspor, dan detail.
- Validasi dan sanitasi input; proteksi CSRF; rate limiting login; session cookie aman pada hosting HTTPS.
- Upload gambar: periksa MIME/ukuran, simpan dengan nama aman, cegah eksekusi file, batasi akses penghapusan, dan tangani file rusak.
- Semua file asli dan turunan disimpan privat; endpoint media memeriksa publikasi aktif pada setiap akses. Jangan mengekspos path storage, draft, revisi historis, atau snapshot privat melalui URL publik, respons Livewire, HTML, feed, sitemap, dan hasil pencarian. Preview internal memakai autentikasi, policy, serta cache privat/no-store; URL bertanda tangan saja bukan pengganti izin.
- Konten nonpublik pada URL publik memberi 404 tanpa membocorkan keberadaannya; akses internal tanpa izin memberi 403. Arsip dan penggantian publikasi membatalkan akses media yang tidak lagi dipakai publikasi aktif serta menginvalidasi cache aplikasi/CDN. Salinan yang sudah diunduh pengguna tidak dapat ditarik kembali.
- File yang sudah direferensikan revisi beku tidak boleh ditimpa; penggantian menghasilkan file baru dan review ulang. Jika file dipakai beberapa publikasi aktif, pengarsipan satu konten tidak menutup pemakaian lain yang sah. Penghapusan file aktif ditolak sampai referensinya diselesaikan.
- Audit aksi penting dan uji backup sebelum demo online; hindari data asli dalam file contoh, screenshot, atau repository.
- Gunakan akun contoh dengan kredensial demo yang dapat dirotasi; jangan menaruh kredensial tetap di repo publik.

## 9. Standar UI/UX dan aksesibilitas
**Prinsip:** modern dan energik, tetapi bersih; mobile-first, keterbacaan tinggi, dan navigasi minim kebingungan. Identitas sementara dapat diganti tanpa merombak komponen.

- Komponen responsive dari viewport kecil; uji minimal 360, 390, 768, dan 1280px.
- Teks isi nyaman dibaca, hirarki heading konsisten, ruang kosong memadai, dan tombol mudah disentuh.
- Kombinasi warna akhir diuji kontrastnya; jangan bergantung pada warna saja untuk status.
- Keyboard focus jelas, urutan tab logis, skip link, label formulir, pesan kesalahan informatif, dan alt text.
- Mendukung zoom sampai 200% dan reflow tanpa hilangnya informasi penting; hindari animasi berlebihan dan hormati reduced motion.
- Jadwal mendatang terlihat jelas di beranda; kalender tetap punya tampilan daftar bagi pengguna HP.
- Target kesesuaian WCAG 2.2 Level AA; kelulusan hanya dinyatakan setelah pengujian manual dan otomatis.
- Gunakan design tokens untuk warna/logo/typography dan dokumentasikan komponen agar dashboard serta halaman publik konsisten.

## 10. Arsitektur teknis
- Editor: VS Code; AI coding assistant: Codex; panduan audit UI: Impeccable.
- Backend: PHP dan Laravel; controller/action/service sesuai tanggung jawab.
- View: Blade; interaksi server-driven dengan Livewire.
- Styling: Tailwind CSS, komponen desain yang dapat digunakan ulang.
- Data: MySQL lokal; migrations, model, factories, dan seeders untuk data simulasi.
- Build aset: tool build bawaan starter Laravel yang dipilih saat inisialisasi proyek.
- Aplikasi terpadu monolith untuk menghindari kompleksitas API terpisah yang belum diperlukan.
- Proyek Airlow memiliki direktori, database, konfigurasi, dan git repository terpisah dari proyek Leihari.

## 11. Persyaratan nonfungsional
- **Kinerja:** gambar responsif/terkompresi, lazy loading bila tepat, minim aset berlebihan, dan pengukuran Lighthouse saat uji.
- **Keandalan:** validasi state, error handling, empty state, dan pengujian otomatis fitur penting.
- **Kemudahan pemeliharaan:** penamaan konsisten, README, migrasi yang dapat diulang, seed data contoh, dan tanpa rahasia di git.
- **Aksesibilitas:** sasaran WCAG 2.2 AA dengan uji keyboard, zoom, screen reader, dan alat audit; hasil perlu didokumentasikan.
- **Privasi:** seluruh anggota dan identitas kontak adalah fiktif. Tidak ada data asli saat fase belajar.
- **Hosting demo:** HTTPS, `APP_DEBUG=false`, konfigurasi .env aman, izin storage, backup, dan akses terbatas jika belum siap dibuka publik.

## 12. Skenario uji dan kriteria penerimaan MVP
- Pengunjung di HP dapat menemukan jadwal terdekat, membaca detail kegiatan, dan berpindah ke berita/galeri tanpa login.
- Admin bisa login, membuat Pengurus, dan membatasi aksesnya.
- Pengurus bisa membuat draft berita/kegiatan; draft tetap privat saat pending_review dan approved, sampai Admin melakukan aksi Terbitkan terpisah.
- Admin bisa mengembalikan draft dengan alasan; Pengurus melihat alasan dan mengajukan revisi.
- Hanya status published yang terlihat melalui URL publik; konten draft tidak dapat diambil dengan menebak slug.
- Revisi v2 dari konten terbit v1 tidak mengubah publikasi selama draft, pending_review, maupun approved; hanya Terbitkan v2 mengganti tampilan. Uji juga revisi oleh Admin, keputusan paralel, penerbitan revisi kedaluwarsa, dan revisi milik konten lain.
- Uji URL langsung file asli/thumbnail/optimized: media approved yang hanya ada pada draft tetap tertutup. Album/kegiatan diarsipkan menutup akses yang tidak punya pemakaian publik aktif lain; preview privat tidak bocor melalui cache.
- Pemilik/penugasan tidak dapat dimanipulasi Pengurus; slug stabil dan benturan ditolak/ditangani; waktu publikasi berbeda dari waktu persetujuan. Revisi profil organisasi dan album juga tidak mengubah versi terbit sebelum review dan penerbitan ulang.
- Pengurus tidak bisa membuka impor/ekspor atau data anggota yang bukan nama/kelompok/status, termasuk dengan URL langsung.
- Admin bisa membuat, memperbarui, dan mencari anggota simulasi.
- Upload gambar yang sah berhasil; file tidak sah ditolak; thumbnail dan alt text bekerja.
- Form menampilkan pesan validasi; logout mengakhiri sesi; login berulang dibatasi.
- Di viewport 360/390/768/1280px tidak ada overflow horizontal tidak disengaja atau fitur terpotong.
- Uji otomatis dan uji manual aksesibilitas dilakukan; setiap kegagalan diberi tindak lanjut, tanpa mengklaim lulus WCAG sebelum dibuktikan.

## 13. Rencana kerja dan prioritas implementasi
**Fase 0 — Persiapan:** buat repository proyek Airlow yang terpisah, setup Laravel/Livewire/Tailwind/MySQL, gitignore dan README, aturan kerja Codex. Tidak menyentuh proyek Leihari.

**Fase 1 — Fondasi:** autentikasi tanpa register, role/policy, layout publik/dashboard, design tokens, struktur navigation, data simulasi.

**Fase 2 — Konten utama:** bangun satu alur berita lengkap dengan revisi, persetujuan, penerbitan terpisah, dan uji akses publik terlebih dahulu; gunakan fondasi yang sama untuk profil organisasi, pengurus, bidang, program kerja, kegiatan/kalender, berita/pengumuman, detail publik.

**Fase 3 — Workflow dan data:** lengkapi review/penerbitan di semua modul, histori keputusan dan penerbitan, CRUD anggota terbatas, upload privat, album dan thumbnail. Logging minimum aksi penting sejak MVP; dashboard audit lengkap tetap lanjutan.

**Fase 4 — Hardening dan lanjutan:** impor Excel/CSV, audit log, backup/pemulihan, tes keamanan, aksesibilitas, browser dan performa.

**Fase 5 — Demo:** review konten dan placeholder, pengujian akhir, konfigurasi hosting demo (opsional), panduan pengurus, bahan presentasi.

Fase boleh dipecah menjadi tugas kecil; setiap perubahan kode wajib direview dan diuji. Gunakan Codex untuk implementasi per langkah dan Impeccable untuk kritik desain, bukan sebagai pengganti pengujian browser.

## 14. Risiko dan mitigasi
- **Cakupan terlalu besar untuk pemula:** wajibkan MVP yang terukur; impor, backup terjadwal, dan hardening lanjutan boleh diselesaikan kemudian, tanpa memasukkan data asli.
- **AI menghasilkan kode yang belum teruji:** tinjau diff, jalankan test, dan periksa otorisasi sebelum menerima perubahan.
- **Data dan identitas simulasi disalahartikan sebagai resmi:** tampilkan label prototype, gunakan placeholder, minta persetujuan sebelum pemakaian nyata.
- **Pengurus bingung dengan dashboard:** gunakan alur sederhana, bahasa Indonesia, empty states, bantuan singkat, dan pengujian pengguna.
- **Koneksi lambat:** optimasi foto, navigasi ringan, hindari animasi/JavaScript yang tidak perlu.
- **Keamanan hosting demo:** gunakan akun simulasi, HTTPS, kredensial aman, dan pembatasan akses jika hardening belum tuntas.

## 15. Definisi selesai dan serah terima
MVP dianggap selesai jika semua kriteria penerimaan bagian 12 telah diuji, tidak ada masalah kritis keamanan/akses, konten diberi label simulasi, migrasi dan seeder bisa dijalankan ulang di lingkungan baru, serta README menjelaskan cara instalasi, menjalankan, testing, dan akun demo secara aman. Dokumentasi penggunaan dashboard serta daftar keterbatasan yang belum dibangun disertakan.

## 16. Catatan keputusan proyek
Keputusan yang telah disepakati: halaman publik + dashboard, anggota sederhana, dua peran Admin/Pengurus, kalender + daftar kegiatan, berita/pengumuman/galeri, profil lengkap, persetujuan Admin, desain modern-energik, navigasi hybrid, mobile-first dan target WCAG 2.2 AA, Laravel/Livewire/Tailwind/MySQL, lokal dahulu, keamanan standar profesional, akun internal dibuat Admin, anggota input manual + impor CSV/Excel, data anggota untuk Pengurus terbatas, upload foto teroptimasi, MVP fungsional bertahap, serta identitas sementara.

**Status persetujuan PRD:** Rancangan siap ditinjau. Belum merupakan persetujuan untuk mengimplementasikan kode, memakai identitas asli, atau mempublikasikan website resmi.

## 17. Keputusan lanjutan dan changelog
Masih perlu keputusan sebelum implementasi terkait: batas ukuran/dimensi/format gambar dan SLA proses optimasi; retensi media/audit/backup dan pemulihan; aturan overlap masa bakti/duplikat jabatan; hosting demo dan konfigurasi cache yang dapat mencabut akses. Data resmi tetap placeholder. Demo memakai Asia/Jayapura; pemakaian nyata memerlukan konfirmasi zona waktu organisasi. Prosedur penyerahan/pemulihan kredensial akun internal serta kebutuhan reset password mandiri masih perlu ditetapkan. 2FA/passkeys tidak ditambahkan sebagai kewajiban MVP tanpa keputusan cakupan tersendiri. Keputusan ini tidak mengubah pemisahan persetujuan dan penerbitan.

| Versi | Tanggal | Perubahan |
|---|---|---|
| 1.1 | 24 Oktober 2026 | Pisahkan persetujuan/penerbitan; kamus status dua lingkup; revisi wajib termasuk Admin; slug/waktu/kepemilikan; media privat; sinkronisasi entitas, rute, kriteria uji, dan fase kerja. Fitur MVP/lanjutan serta identitas visual dipertahankan. |
| 1.0 | 24 Oktober 2026 | Rancangan awal kebutuhan, cakupan, keamanan, dan kriteria penerimaan. |
