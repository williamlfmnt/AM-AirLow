# WIREFRAME & ALUR LAYAR — PROTOTYPE ANGKATAN MUDA AIRLOW
Versi: 1.1 (wireframe low-fidelity, diselaraskan) | 24 Oktober 2026
Sesuai PRD v1.1, ERD_Prototype v1.1 dan Design System v1.1. Semua data adalah simulasi. Wireframe adalah struktur, bukan tangkapan layar atau halaman yang sudah jadi. Pembaruan ini hanya rancangan, bukan implementasi UI.

## 0. Kamus status dan alur bersama
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

Alur: draft → Ajukan persetujuan → pending_review → Setujui → approved → **Terbitkan melalui aksi Admin terpisah** → publikasi published. Minta revisi/Tolak menghasilkan revision_requested/rejected dengan alasan; tindak lanjut membuat draft versi baru. Untuk revisi approved yang belum pernah diterbitkan, bantuan **Disetujui — belum diterbitkan**. Konten dapat tetap published v1 saat revisi v2 berada pada salah satu status revisi; v1 baru diganti setelah v2 diterbitkan. Berlaku juga bagi revisi Admin; Admin boleh menyetujui karya sendiri melalui aksi eksplisit, tanpa syarat reviewer kedua.

Moderasi media memakai pending_review/approved/rejected dengan label yang sama. Keterangan Ditampilkan pada publikasi aktif berasal pemakaian pada versi aktif, bukan approved saja. Status anggota/program/impor adalah domain berbeda.

## A. Sitemap publik (hybrid)
`/` Beranda → `/tentang`, `/pengurus`, `/program-kerja`, `/kegiatan`, `/berita`, `/pengumuman`, `/galeri`, `/kontak`.
Detail: `/program-kerja/{slug}`, `/kegiatan/{slug}`, `/berita/{slug}`, `/pengumuman/{slug}`, `/galeri/{slug}`. Slug stabil setelah terbit pertama; perubahan judul tidak mengubah URL. Konten unpublished/archived, draft/approved yang belum diterbitkan, dan versi historis tidak dibuka lewat URL publik (404 tanpa kebocoran metadata). Preview berbeda dan hanya internal.

### WF-P01 Beranda — HP (prioritas pertama)
```
┌──────────────────────────────┐
│ AM AIRLOW        [Menu ☰]    │
│ Prototype · Data simulasi    │
├──────────────────────────────┤
│ KOMUNITAS & PELAYANAN        │
│ Angkatan Muda Airlow         │
│ Pengantar ringkas            │
│ [Lihat Jadwal Kegiatan]      │
├──────────────────────────────┤
│ [Jadwal] [Pengumuman] [Galeri]│
├──────────────────────────────┤
│ Kegiatan Terdekat  Lihat semua│
│ [Tanggal, acara, jam, tempat]│
│ [Kartu kegiatan berikutnya]  │
├──────────────────────────────┤
│ Pengumuman Penting           │
│ [Ringkasan pengumuman]       │
├──────────────────────────────┤
│ Berita Terbaru               │
│ [Foto] Judul · tanggal       │
├──────────────────────────────┤
│ Dokumentasi Kegiatan         │
│ [Foto] [Foto]                │
├──────────────────────────────┤
│ Kontak · footer · Prototype  │
└──────────────────────────────┘
```
Urutan informasi utamakan jadwal; hero jangan mendorong kegiatan terlalu jauh dari layar pertama. Elemen interaktif berupa tautan/tombol sungguhan ketika diimplementasikan. Desktop: hero dua kolom hanya jika konten dan foto relevan; kegiatan memakai grid fleksibel; jangan menambah dekorasi acak.

### WF-P02 Kegiatan
Header + judul + toggle `Daftar | Kalender` + filter bulan/kategori + daftar kartu atau kalender; klik tanggal memperlihatkan daftar acara tanggal itu; kosong tampilkan penjelasan dan tautan kembali. Detail kegiatan: judul, tanggal lengkap + WIT, tempat, deskripsi, media relevan; hanya item published yang publik.

Daftar/kalender membaca versi publik aktif saja, termasuk tanggal/lokasi/foto. Ada kontrol bulan sebelumnya/berikutnya, Kembali ke bulan ini, dan Hapus filter. Keyboard dapat mencapai kontrol/tanggal dan membaca daftar acara tanggal terpilih; tanggal dengan banyak acara menampilkan jumlah serta daftar, bukan informasi terpotong. Acara lintas hari dijelaskan dengan rentang tanggal/jam. State tanpa hasil membedakan belum ada kegiatan dari filter tanpa kecocokan. Daftar tetap alternatif penuh pada HP dan pembaca layar.

### WF-P03 Berita & Pengumuman
Daftar kartu ringkas, pencarian/penyaringan seperlunya, masing-masing ke halaman detail semantik. Artikel: judul, tanggal publikasi, penulis organisasi bila layak, gambar utama alt bermakna, isi, tautan kembali. Pengumuman penting ditampilkan lebih menonjol namun tanpa marquee/animasi distraktif.

Tanggal Terbit pertama berasal penerbitan pertama; Diperbarui hanya setelah revisi pengganti diterbitkan, bukan saat disetujui/disimpan. Tampilkan WIT. Penonjolan pengumuman mengikuti is_important pada revisi aktif, sehingga draft perubahan prioritas tidak mengubah beranda.

### WF-P04 Galeri
Album berdasarkan kegiatan, sampul dan jumlah foto; detail album menampilkan thumbnail, deskripsi kegiatan, alt text. Pada mobile satu/dua kolom sesuai ukuran; jaga target sentuh. Galeri hanya dari snapshot album published; bila terhubung kegiatan, kegiatan dalam snapshot juga harus published. Foto wajib approved dan tercatat pada snapshot aktif. Sampul dipilih Admin dari foto sah atau foto approved pertama sesuai urutan snapshot. Jumlah/sampul/caption tidak membaca draft album terbaru. File asli/thumbnail/optimized nonpublik tidak dapat diambil lewat URL langsung.

### WF-P05 Profil organisasi
Tentang: sejarah simulasi, visi/misi, bidang. Pengurus: masa bakti → daftar nama/jabatan data fiktif. Program kerja: daftar dan detail, kategori/masa bakti bila tersedia. Kontak: informasi placeholder (jangan tampilkan nomor atau alamat yang dikarang seolah resmi).

Seluruhnya membaca snapshot paket organisasi published. Program detail /program-kerja/{slug} memakai isi snapshot aktif, bukan data kerja. Nama/jabatan publik tidak diasumsikan akun login; daftar anggota internal tidak ditautkan. Bila paket organisasi belum terbit, tampilkan halaman kosong publik yang jujur tanpa mengambil draft.

## B. Dashboard internal (Adaptive)
### WF-D01 Login
```
┌──────────────────────────────┐
│ AM AIRLOW · Portal Pengurus  │
│ [Email____________________]  │
│ [Password_________________]  │
│ [Masuk]                      │
│ Pesan kesalahan/keamanan     │
│ Prototype · akun demo       │
└──────────────────────────────┘
```
Tidak ada registrasi publik. Jangan bocorkan detail akun terdaftar melalui pesan error.

Setelah login arahkan /dashboard; tampilkan error kredensial umum, pembatasan percobaan, dan akun tidak dapat mengakses portal tanpa membocorkan rincian. Akun nonaktif tidak boleh masuk/menjalankan aksi internal. Menu akun menyediakan Keluar yang mengakhiri sesi. Keputusan UI pemulihan akun/2FA/passkeys dibahas pada §G; jangan memasukkan fitur tambahan tersebut sebagai kewajiban MVP tanpa keputusan.

### WF-D02 Ringkasan Dashboard — desktop
```
┌─────────────────────────────────────────────────────────┐
│ SIDEBAR                 │ TOP BAR: halaman + akun         │
│ Ringkasan               ├────────────────────────────────┤
│ Kegiatan                │ [Draft] [Review] [Agenda]      │
│ Berita                  │                                │
│ Pengumuman              │ Pekerjaan yang perlu tindakan  │
│ Galeri                  │ [Daftar item & status]          │
│ Anggota                 │                                │
│ (Admin: Persetujuan)    │ [Tambah Kegiatan] [Buat Berita]│
│ (Admin: Pengguna)       │                                │
└─────────────────────────────────────────────────────────┘
```
Di HP: sidebar menjadi menu yang dapat dibuka/tutup; ringkasan, daftar kerja, dan aksi menjadi satu kolom. Jangan menampilkan kartu statistik sebagai dekorasi; setiap angka terkait data relevan.

Ringkasan dan filter memakai label Menunggu persetujuan; Admin juga mendapat daftar **Disetujui — belum diterbitkan** yang mengarah ke aksi Terbitkan. Pengurus hanya melihat pekerjaan milik/ditugaskan. Sidebar Admin menambah Organisasi (kelompok profil/bidang/masa bakti/kepengurusan/program), Pengaturan, serta Audit pada fase lanjutan. Kelompok Organisasi mencegah daftar menu sejajar terlalu panjang. Dua indikator contoh: Versi publik Terbit v1 / Revisi terbaru Menunggu persetujuan v2.

### WF-D03 Kelola konten dan kegiatan
Daftar + pencarian + filter status revisi dan publikasi terpisah + tombol Tambah; pada HP item menjadi kartu berlabel. Form: judul, tanggal/waktu WIT, tempat, jenis, deskripsi, foto opsional; berita/pengumuman menyesuaikan field termasuk penanda Penting untuk pengumuman. Aksi Simpan draft, Preview internal, Ajukan persetujuan. Feedback jelas; simpan bukan ajukan atau terbitkan.

Header editor: nomor versi, owner/penugasan, author revisi, dua status, URL stabil, dan waktu pengajuan/keputusan/penerbitan. Owner/penugasan hanya dapat diubah Admin; created_by tetap. Admin mengatur slug sebelum terbit pertama; sesudahnya hanya-baca. Pengurus tidak dapat memanipulasi pemilik melalui form atau request. Draft merupakan satu-satunya isi versi yang dapat disunting; revisi diajukan/terminal menampilkan Baca versi dan Buat revisi baru bila berizin. Riwayat memperlihatkan alasan revisi/penolakan serta versi yang sudah dipublikasikan, bukan menimpa keputusan lama.

Preview berlabel **Preview privat — belum diterbitkan**, memakai sesi/policy, tanpa tautan berbagi publik. Untuk konten terbit, ada tautan Lihat versi publik yang terpisah. Tombol Batal/Kembali, pesan perubahan belum tersimpan, input tetap saat validasi gagal, dan penanganan sesi berakhir tersedia. Konflik versi mengharuskan muat ulang/rekonsiliasi; tidak menimpa diam-diam.

### WF-D04 Persetujuan Admin
Daftar Menunggu persetujuan; halaman per item memperlihatkan nomor revisi, author, isi yang dibekukan, perubahan terhadap versi publik, media, status dan komentar. Aksi Admin Setujui, Minta revisi, Tolak; dua terakhir wajib alasan. Setelah Setujui tampil **Disetujui. Belum ditampilkan ke publik.** dan item masuk daftar Disetujui — belum diterbitkan. Jangan menggabungkan Setujui dengan Terbitkan.

Langkah penerbitan terpisah menampilkan versi yang akan terbit, versi publik yang diganti (bila ada), kelayakan media, serta tombol Terbitkan. Media belum disetujui/turunan belum siap atau versi parent berubah memberi alasan dan langkah pemulihan; backend tetap menolak walau tombol dimanipulasi. Sukses menampilkan nomor versi, waktu WIT, penerbit, dan Lihat versi publik. Pengurus melihat status/alasan milik/ditugaskan tanpa aksi Admin.

Riwayat memisahkan keputusan persetujuan dari penerbitan. Arsipkan/Tarik terbit meminta alasan dan konfirmasi dampak; tampilkan bahwa album terkait juga dapat berhenti publik. Penerbitan kembali tetap aksi eksplisit untuk versi approved yang dipilih. Klik ganda tidak menggandakan histori; konflik penerbitan tidak boleh tampak sukses.

### WF-D05 Anggota
Admin: daftar+filter+CRUD manual menggunakan data fiktif (impor/ekspor pada fase lanjutan). Pengurus: daftar **hanya** nama, kelompok, dan status; tidak menampilkan/menyertakan field privat dalam data respons. Tidak ada laman anggota publik.

Admin memiliki pencarian, filter kelompok/status, paginasi, form tambah/edit, validasi kode anggota unik, dan konfirmasi penghapusan lunak. Pengurus tidak mendapat kode anggota, gender, tanggal bergabung, atau catatan dalam HTML/state Livewire/JSON, bukan sekadar kolom tersembunyi. Pengelolaan kelompok disediakan dalam modul Anggota untuk Admin; kelompok yang masih dipakai tidak dapat dihapus. Tidak ada tombol impor/ekspor aktif sebelum fase lanjutan.

### WF-D06 Upload foto
Dialog/form pilih file + preview + alt text + kaitkan ke kegiatan/album + hasil optimasi/thumbnail. Tampilkan kesalahan ukuran/format dan progres upload. Jangan menghapus foto yang terkait tanpa kebijakan jelas.

Tampilkan status moderasi pending_review/approved/rejected beserta alasan penolakan. Media approved tanpa pemakaian publik diberi keterangan Belum digunakan pada publikasi. Label Ditampilkan pada publikasi aktif hanya bila ada referensi aktif yang sah. Pengurus melihat unggahan yang diizinkan; Admin dapat meninjau foto tanpa membuat berita. Approval foto tidak menerbitkan album/konten. Bila file dipakai versi beku, aksi Ganti membuat file baru, bukan menimpa file lama. Penghapusan file yang dipakai publikasi aktif ditolak dengan daftar konteks yang boleh dilihat pengguna.

### WF-D07 Organisasi: profil, bidang, masa bakti, kepengurusan, program
Admin-only di /dashboard/organisasi. Subnavigasi Profil & Kontak, Bidang, Masa bakti, Kepengurusan, Program kerja; bukan lima menu utama baru. Form sesuai kamus ERD, urutan tampilan, logo/foto disetujui, status/masa bakti, validasi tanggal dan nama/slug unik. Kepengurusan menyimpan nama simulasi terpisah dari users; program memiliki halaman detail dan slug stabil.

Perubahan data kerja → Simpan revisi paket organisasi → Preview privat seluruh halaman terdampak → Ajukan persetujuan → Setujui → Terbitkan melalui aksi terpisah. Paket menampilkan nomor versi, ringkasan perubahan, waktu/aktor dan referensi foto; Admin boleh menjalankan tiap aksi sendiri secara eksplisit. Versi publik lama tetap tampil pada setiap tahap sebelum penerbitan. Menghapus/mengubah data kerja tidak mengubah snapshot terbit. Validasi masa bakti aktif tunggal dan kelompok referensi; konflik organisasi tidak diterima.

### WF-D08 Pengguna dan penugasan
Admin-only di /dashboard/pengguna: daftar/pencarian, buat akun internal, pilih role Admin/Pengurus, aktif/nonaktif, dan validasi email unik. Tidak ada pendaftaran publik atau penghapusan akun yang merusak histori. Jangan tampilkan password/hash/token pada daftar, log, atau respons. Mekanisme penyerahan/reset kredensial menunggu keputusan §G; UI tidak memberi kesan email sudah dikirim bila belum ada layanan pengiriman.

Pada detail kegiatan/post, Admin memilih owner dan maksimal satu assigned_editor; tampilkan perbedaan pembuat awal dengan penanggung jawab. Perubahan dicatat dan tidak mengubah penulis revisi/keputusan historis. Pengurus tidak melihat kontrol ini sebagai aksi edit dan tidak bisa menjalankannya lewat URL/action.

### WF-D09 Pengaturan dan histori operasional
Admin-only di /dashboard/pengaturan: ringkasan identitas simulasi dan zona waktu demo WIT; sunting identitas melalui paket Organisasi agar tetap mengikuti penerbitan. Pengaturan operasional yang benar-benar tersedia diberi label jelas; tidak menampilkan editor .env, secret, atau konfigurasi server. Jangan menawarkan penjadwalan publikasi otomatis dalam MVP.

Histori persetujuan/penerbitan minimum melekat pada detail konten sejak MVP. /dashboard/audit-log dan antarmuka backup/impor/ekspor merupakan layar lanjutan: audit dengan aktor/aksi/target/waktu dan metadata aman; impor dengan pemetaan, preview, validasi duplikat/error per baris; ekspor dengan field yang diizinkan; backup dengan status dan hasil uji pemulihan. Fitur lanjutan tidak dijadikan syarat demo MVP lokal; logging minimum dan uji pemulihan sebelum demo online tetap wajib.

### WF-D10 Pengelolaan album
Admin-only untuk daftar/edit album di /dashboard/galeri; Pengurus tetap dapat mengunggah media melalui WF-D06 sesuai izin. Form album: judul/slug, kegiatan terkait opsional, deskripsi, foto disetujui, sampul, caption dan alt. Simpan revisi snapshot album → Preview privat → Ajukan persetujuan → Setujui → Terbitkan terpisah. Foto belum disetujui atau kegiatan terkait belum publik menghalangi penerbitan. Edit album terbit membuat versi baru dan mempertahankan sampul/isi publik lama. Pengurutan dasar snapshot tetap stabil; UI pengurutan kaya/pengelompokan lanjutan mengikuti FR-14.

## C. Matriks breakpoint dan state
- Mobile rancangan: 360, 390, 430 CSS px; juga uji 320px bila memungkinkan.
- Tablet: 768px; Desktop: 1280, 1440px. Breakpoint implementasi berdasarkan konten, bukan sekadar ukuran perangkat.
- Keyboard: tab order, fokus, menu toggle/Escape, skip link, link tujuan jelas; drawer/modal mengelola fokus dan mengembalikannya ke pemicu. Kalender memiliki alternatif daftar penuh.
- Zoom dan preferensi aksesibilitas: zoom 200% dan reflow, prefers-reduced-motion, validasi dengan alat dan pemeriksaan manual.
- State: loading, empty, validasi/error upload, 403 internal, 404 publik tanpa data privat, 500 aman, sukses; seluruh status pada §0; approved belum diterbitkan, media belum siap, konflik versi, sesi berakhir dan perubahan belum tersimpan. Uji koneksi lambat/gagal, retry tanpa duplikasi dan pengumuman status bagi pembaca layar.

## D. Urutan implementasi desain
1. Tinjau struktur dan konten setiap layar dengan kelompok/pengurus (tanpa memakai data asli).
2. Periksa hirarki mobile P01 dan D02; perbaiki alur yang membingungkan.
3. Buat komponen dasar (header/nav, buttons, form, cards, tables, status, modals) ketika fase coding resmi dimulai.
4. Implementasi dengan Codex; gunakan Impeccable untuk shape/critique/audit setelah halaman tersedia; verifikasi browser nyata.

## E. Checklist sebelum desain disetujui
[ ] Semua halaman PRD tercakup; [ ] shortcut jadwal mudah ditemukan; [ ] menu mobile berlabel; [ ] role Admin/Pengurus tidak disamakan; [ ] form dan empty states; [ ] Setujui tidak menerbitkan; [ ] dua status/versi jelas; [ ] revisi Admin mengikuti alur sama; [ ] URL draft/file privat tertutup; [ ] data simulasi ditandai; [ ] kontras/sentuh/keyboard rencana uji tercatat; [ ] tidak ada fitur di luar MVP yang dipaksakan.

## F. Skenario walkthrough penyelarasan
1. Pengurus membuat berita v1, mengajukan, Admin menyetujui: tidak ada URL publik aktif. Admin Terbitkan: v1 baru terlihat.
2. Pengurus atau Admin membuat v2 dari v1 terbit; setelah v2 approved, v1 tetap tampil beserta medianya. Terbitkan v2 baru mengganti versi publik.
3. URL langsung draft/approved, preview tanpa izin, original/thumbnail/optimized privat menghasilkan penolakan tanpa data privat; cache tidak menyajikan preview. Pengurus yang mengakses fungsi Admin mendapat 403.
4. Admin mengubah paket organisasi/album: data kerja dan snapshot draft tidak mengubah halaman publik sampai review dan penerbitan ulang.
5. Arsip kegiatan menutup detail dan album terkait; media masih boleh publik jika dipakai publikasi aktif lain. Terbitkan kembali dicatat sebagai aksi baru setelah validasi.
6. Pengurus melihat nama/kelompok/status anggota saja; field privat tidak ada di respons. Tidak dapat memalsukan owner, penugasan, reviewer atau waktu terbit.
7. Lakukan walkthrough HP dan keyboard untuk editor → review → disetujui belum diterbitkan → Terbitkan, termasuk kegagalan media, konflik versi dan sesi berakhir. Ini rencana uji, bukan hasil pengujian UI jadi.

## G. Keputusan tersisa dan changelog
- Tentukan batas ukuran/dimensi/format upload dan waktu proses optimasi; pesan error mengikuti keputusan tersebut (PRD §17, ERD §9).
- Tentukan prosedur penyerahan/pemulihan kredensial akun Admin/Pengurus dan apakah reset password mandiri diperlukan. UI 2FA/passkeys memerlukan keputusan tersendiri; belum ditambahkan sebagai fitur wajib PRD.
- Konfirmasi aturan overlap masa bakti/duplikat jabatan, retensi backup/media/audit, serta hosting dan invalidasi cache. Demo tetap data simulasi, Asia/Jayapura; zona waktu penggunaan nyata dikonfirmasi kemudian.
- Finalisasi token status/border dan uji kontras/usability saat implementasi. Palet, font, radius, spacing, struktur hybrid/adaptif, serta target WCAG 2.2 AA tidak diganti.

| Versi | Tanggal | Perubahan |
|---|---|---|
| 1.1 | 24 Oktober 2026 | Kamus status dua lingkup, review/penerbitan terpisah, revisi terbit termasuk Admin, privasi URL/media, detail kalender/editor/review, layar organisasi/pengguna/pengaturan/album, alur histori dan walkthrough. Fitur lanjutan tetap terpisah dan identitas visual dipertahankan. |
| 1.0 | 24 Oktober 2026 | Sitemap dan wireframe low-fidelity publik/dashboard awal. |
