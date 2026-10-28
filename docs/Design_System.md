# DESIGN SYSTEM — PROTOTYPE ANGKATAN MUDA AIRLOW
Versi: 1.1 (penyelarasan perencanaan) | 24 Oktober 2026 | Status: belum diimplementasikan

## 1. Konteks dan prinsip
Rujukan: PRD v1.1, ERD_Prototype v1.1, dan Wireframe v1.1. Website prototype/data simulasi, bukan layanan organisasi resmi. Dua antarmuka: website publik untuk membaca informasi; dashboard internal untuk mengoperasikan manajemen konten. Mobile-first, karakter modern dan energik, visual sederhana; target WCAG 2.2 AA (target, bukan klaim sertifikasi).

Prinsip: tugas inti mudah ditemukan; informasi lebih penting daripada dekorasi; pengalaman HP utama, desktop tetap matang terutama dashboard; desain konsisten; setiap aksi dan status punya label teks; formulir menjelaskan kesalahan dan memberi umpan balik; konten resmi tidak dipalsukan.

## 2. Identitas sementara
Nama kerja: Angkatan Muda Airlow. Logo: placeholder berlabel AM AIRLOW; mudah diganti. Tidak menggunakan lambang organisasi atau informasi kepengurusan resmi tanpa persetujuan. Tampilkan penanda `Prototype — Data simulasi` yang mudah ditemukan.

### Warna dasar (telah dipilih)
- `primary-700`: `#184A9C` — navigasi, tombol utama, link prioritas.
- `accent-500`: `#EF813F` — aksen dekoratif, indikator, bukan teks kecil pada putih.
- `canvas`: `#F7F9FC` — latar halaman.
- `ink`: `#17263D` — teks utama.

### Token pendukung sementara (usulan, perlu evaluasi kontras)
- `surface`: `#FFFFFF`
- `border`: `#D7E0EB`
- `muted`: `#475569`
- `primary-hover`: `#123B7D`
- `focus-ring`: `#184A9C` dengan offset yang terlihat
- `success`, `warning`, `danger`: gunakan ikon+teks; definisikan token saat implementasi dan verifikasi kontras, jangan mengandalkan warna saja.

Kombinasi untuk teks dan kontrol harus diuji terhadap WCAG 2.2 AA; acuan awal minimal 4.5:1 teks biasa dan 3:1 teks besar/komponen yang relevan. Jangan anggap seluruh pasangan warna ini otomatis memenuhi.

## 3. Tipografi (telah dipilih)
- Heading dan identitas: Montserrat (fallback system sans-serif).
- Body, navigasi, tabel, formulir: Source Sans 3 (fallback system sans-serif).
- Skala awal desktop/mobile fleksibel: hero 32–44px, H1 30–36px, H2 24–28px, H3 20–22px, body 16–18px, label 16px, metadata 14–16px.
- Body line-height 1.5–1.7. Perhatikan reflow pada zoom 200%, tidak membatasi pembesaran. Hindari penggunaan uppercase panjang. Tidak lebih dari dua keluarga font dalam antarmuka biasa.

## 4. Komponen Balanced Modern (telah dipilih)
- Radius: tombol/input 8px; kartu 12px; panel besar 16px. Hindari pill di setiap elemen.
- Spacing berbasis kelipatan 4px: 4/8/12/16/24/32/48/64px. Gunakan pemisahan section yang jelas dan jarak konsisten.
- Target ukuran sentuh: rancang minimal sekitar 44×44 CSS px sebagai target internal yang nyaman; uji untuk WCAG 2.2 AA dan toleransi jarak.
- Tombol: primary biru teks putih; secondary outline; destructive hanya untuk aksi berisiko; disabled bukan satu-satunya cara menjelaskan kondisi.
- Kartu kegiatan: judul, waktu lokal WIT, tempat, status publikasi bila internal, tautan detail. Tanggal lengkap jangan dipadatkan sehingga pecah sulit dipahami.
- Input: label eksplisit, hint jika dibutuhkan, error dekat field, tanda wajib jelas, konfirmasi hanya pada tindakan destruktif.
- Tabel dashboard: header deskriptif, alternatif kartu bertumpuk di layar kecil, pencarian dan filter dengan label.
- Status revisi dan publikasi menggunakan kamus §4.1; tampilkan dua badge berlabel lingkup, bukan satu badge yang menimpa status versi publik. Teks wajib; warna hanya pelengkap.
- Motion: seperlunya, hormati prefers-reduced-motion, hindari efek bounce/animasi terus menerus.
- Galeri: gambar dengan alt text bermakna, thumbnail teroptimasi, tidak mengorbankan keterbacaan.

### 4.1 Kamus status bersama dan aksi
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

Contoh: **Versi publik: Terbit · v1** dan **Revisi terbaru: Menunggu persetujuan · v2**. Revisi approved yang belum pernah diterbitkan memakai bantuan **Disetujui — belum diterbitkan**. Revisi yang sedang tampil tetap approved dari sisi review; label Terbit berasal status publikasi dan penunjuk versi aktif. Jangan menandai semua revisi historis sebagai publik.

- `Ajukan persetujuan`: penulis berizin, hanya draft. Versi yang diajukan dibekukan; perbaikan membuat draft versi baru.
- `Setujui`, `Minta revisi`, `Tolak`: hanya Admin pada pending_review; dua aksi terakhir membutuhkan alasan. Setelah Setujui: **Disetujui. Belum ditampilkan ke publik.**
- `Terbitkan`: aksi Admin yang terpisah, hanya untuk approved yang lolos pemeriksaan media dan versi. Ringkas target versi dan versi yang digantikan, lalu tampilkan hasil **Versi v2 diterbitkan**. Tidak perlu konfirmasi generik untuk setiap aksi non-destruktif; target harus jelas.
- `Arsipkan / Tarik terbit`: Admin, alasan wajib dan konfirmasi dampak akses; tampilkan cara kembali yang tersedia. Terbitkan kembali tetap aksi eksplisit dengan validasi ulang.
- Pengurus melihat status/alasan konten miliknya atau yang ditugaskan, tanpa kontrol persetujuan/penerbitan. Admin boleh menyetujui karya sendiri melalui aksi eksplisit; setiap revisi Admin tetap mengikuti review dan penerbitan terpisah.
- Moderasi media: `pending_review` = Menunggu persetujuan, `approved` = Disetujui, `rejected` = Ditolak. Tambahkan keterangan **Belum digunakan pada publikasi** atau **Ditampilkan pada publikasi aktif**, berdasarkan referensi versi aktif; ini informasi turunan, bukan enum moderasi tambahan.

## 5. Navigasi publik (telah dipilih)
Arsitektur hybrid: beranda ringkas dengan akses cepat Jadwal, Pengumuman, Galeri; halaman lengkap terpisah.
Mobile: header merek + tombol `Menu` berlabel dan status expand; saat membuka menu menampilkan Tentang, Pengurus, Program Kerja, Kegiatan, Berita, Pengumuman, Galeri, Kontak. Shortcut di beranda bukan duplikasi menu permanen. Desktop: navigasi langsung yang jelas, kelompokkan bila ruang tidak cukup. Setiap halaman punya satu H1, breadcrumb saat struktur mendalam, indikator halaman aktif, tautan kembali. Konten primer dalam beranda: kegiatan terdekat, pengumuman penting, berita terbaru, akses galeri.

## 6. Dashboard (Adaptive Dashboard; telah dipilih)
Desktop: sidebar berlabel teks untuk Ringkasan, Kegiatan, Berita, Pengumuman, Galeri, Anggota; fitur Admin: Persetujuan, Organisasi, Pengguna, Audit (lanjutan), Pengaturan. Organisasi mengelompokkan profil/kontak, bidang, masa bakti, kepengurusan, dan program; hindari menambah semuanya sebagai menu sejajar. Area utama memakai heading dan aksi kontekstual. Mobile: sidebar menjadi drawer/menu berlabel; isi satu kolom, tabel menjadi kartu atau scroll terkontrol tanpa memotong tindakan. Jangan bergantung pada ikon tanpa teks. Hak akses tetap dilindungi backend.

Alur utama: daftar → tambah/edit draft → Preview internal → Ajukan persetujuan → Admin review → Setujui → Disetujui — belum diterbitkan → Terbitkan. Cabang Minta revisi/Tolak menampilkan alasan dan pembuatan versi draft baru. Revisi v2 tidak mengubah v1 yang tampil sampai aksi Terbitkan v2 berhasil, termasuk revisi Admin. Album dan paket organisasi mengikuti urutan sama melalui snapshot Admin-only; penyimpanan data kerja bukan penerbitan.

Ringkasan menampilkan tugas sesuai peran: draft, menunggu persetujuan, disetujui belum diterbitkan (Admin), dan kegiatan mendatang. Daftar menyediakan filter revisi/publikasi yang berbeda. Editor menampilkan owner/penugasan, author versi, waktu pengajuan/keputusan/penerbitan dan nomor versi; Pengurus tidak dapat mengganti pemilik. Slug stabil setelah terbit pertama; tampilkan URL publik hanya bila konten benar-benar published. Waktu UI WIT, data UTC; label Terbit pertama/Diperbarui berdasarkan riwayat penerbitan, bukan waktu simpan draft.

## 7. States, aksesibilitas, dan performa
Desain untuk loading, kosong, validasi gagal, 403, 404, 500, berhasil, belum ada data, koneksi lambat. Form harus mempertahankan input pengguna saat error. Navigasi keyboard lengkap, skip link, fokus terlihat, landmark semantik, label yang jelas, kontras terverifikasi, tata letak tetap dapat digunakan pada viewport kecil dan zoom. Jangan menjanjikan kelulusan WCAG tanpa uji.
Optimasi foto, font self-host/fallback bila layak, ukuran aset terkendali, hindari JS/animasi tak perlu. UI tanpa koneksi tidak boleh pura-pura berhasil menyimpan perubahan.

Tambahkan state: disetujui belum diterbitkan, media belum siap/disetujui, versi kedaluwarsa akibat penyuntingan/penerbitan lain, sesi berakhir, perubahan belum tersimpan, dan upload gagal yang dapat dicoba ulang. Pesan menjelaskan tindakan berikutnya dan mempertahankan input yang masih diizinkan; perubahan versi memerlukan muat ulang/rekonsiliasi, jangan diam-diam menimpa pekerjaan lain. Progres/sukses/error diumumkan secara aksesibel; fokus kembali ke pemicu setelah drawer/modal ditutup.

### 7.1 Pemisahan preview dan akses publik
- Preview internal diberi label **Preview privat — belum diterbitkan**, hanya untuk pengguna yang berizin. Jangan menawarkan tautan publik untuk draft/approved atau menganggap signed URL saja cukup sebagai izin.
- File asli, thumbnail dan optimized mengikuti pemeriksaan publikasi aktif yang sama. Media approved hanya publik ketika dipakai versi aktif yang sah. Album terkait kegiatan yang tidak lagi publik juga tidak tampil; sampul/jumlah foto berasal snapshot album terbit.
- URL publik konten/file nonpublik memakai 404 tanpa judul/thumbnail privat; layar internal terlarang memakai 403. Jangan menanam path storage atau state revisi privat ke halaman publik.
- Arsip/ganti publikasi memperbarui cache dan daftar publik; jangan menjanjikan pencabutan salinan yang sudah diunduh. Pratinjau tidak boleh masuk cache publik, pencarian, sitemap, atau feed.

## 8. Batasan dan sign-off
Ini keputusan desain awal; belum ada mockup final atau uji usability. Konten nama kegiatan, narasi, tanggal, jumlah anggota, dan kontak masih data simulasi. Sebelum coding perlu meninjau wireframe tiap layar kritis, lalu implementasi Codex dengan Impeccable untuk evaluasi dan alat uji browser/aksesibilitas. Dokumen ini tidak mengotorisasi coding atau mengubah proyek lain.

## 9. Keputusan tersisa dan changelog
Token success/warning/danger dan variasi border kontrol masih perlu evaluasi kontras saat implementasi; palet dasar, tipografi, radius, spacing, identitas sementara, dan target WCAG 2.2 AA tetap dipilih. Tinjau batas upload, kinerja proses foto, hosting/cache, serta retensi sesuai PRD §17 dan ERD §9. Pemulihan akun/fitur 2FA-passkeys memerlukan keputusan cakupan sebelum ditambahkan ke alur login; tidak menjadi kewajiban MVP baru.

| Versi | Tanggal | Perubahan |
|---|---|---|
| 1.1 | 24 Oktober 2026 | Kamus status revisi/publikasi, aksi Setujui/Terbitkan terpisah, dua indikator versi, snapshot organisasi/album, state kegagalan dan preview/media privat, kelompok navigasi Organisasi. Identitas visual dan cakupan fitur dipertahankan. |
| 1.0 | 24 Oktober 2026 | Prinsip desain, warna, tipografi, komponen, navigasi, aksesibilitas dan performa awal. |
