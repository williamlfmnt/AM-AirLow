# Audit awal situs publik Airlow

Tanggal: 26 Oktober 2026. Tahap 1 saja; tidak ada perubahan kode aplikasi.

## Cakupan dan metode

Scope ditafsirkan sebagai situs publik, dengan fokus beranda dan prioritas pengenalan organisasi yang sudah dipilih pengguna. Dashboard hanya dipetakan dari rute dan kode, tidak direview secara visual atau dioperasikan dengan akun.

Aturan art direction: tasteskill v2 lokal. PRODUCT.md, README.md, PRD, dan Design System dipakai untuk fakta dan batasan produk. Tidak menggunakan Impeccable sebagai tolok ukur visual pada audit ini.

- Inspector browser nyata dijalankan pada `/`, `/tentang`, `/kegiatan`, `/kabar`, dan `/galeri`, masing-masing pada 1440, 768, dan 390 px. Semua 32 gambar fold/contact-sheet yang dihasilkan sudah dibuka dan diperiksa. Area abu-abu pada contact sheet adalah slot kosong penyusunan gambar, bukan latar website.
- HTTP dan HTML tujuh URL diperiksa, termasuk satu detail berita dan satu detail album. Status semuanya 200. Baseline judul, robots, ID, field, dan URL tautan tersimpan di `public-baseline.json`.
- Rute runtime diverifikasi dengan `artisan route:list --except-vendor --json` menggunakan PHP 8.4.26.
- Aplikasi menyajikan aset Vite hasil build; `public/hot` tidak ada. Tidak melakukan build baru atau mengganti dependency dalam tahap audit.
- Suite publik non-database: 26 tes lulus, 1.195 assertion. Ini bukti pengujian otomatis, bukan pengganti pengujian keyboard/screen reader secara manual.
- Lint dijalankan terhadap beranda, CSS publik, dan JS publik. Linter melaporkan hanya dua file yang dipindai; jangan menganggap Blade sudah tercakup penuh oleh linter sumber.

## 1. Brand dan UI aktual

| Unsur | Implementasi saat audit | Perbandingan dengan dokumen |
|---|---|---|
| Primary | `#184A9C` | Sesuai |
| Accent | `#EF813F` | Sesuai; terlihat pada detail logo dan navigasi aktif |
| Canvas / ink | `#F7F9FC` / `#17263D` | Sesuai |
| Teks sekunder / garis | `#475569` / `#D7E0EB` | Sesuai token pendukung |
| Heading / teks | Montserrat / Source Sans 3, WOFF2 lokal | Sesuai; font termuat pada pemeriksaan beranda |
| Logo | Kotak AM dan wordmark Angkatan Muda Airlow | Placeholder, bukan lambang resmi |
| Tombol / gambar | Tombol primary 8px; foto 12px | Tombol sesuai; foto memakai radius kartu, bukan batas baru yang wajib dipertahankan |
| Ukuran | H1 beranda 56px desktop, 36px ponsel; body 18px | H1 desktop lebih besar daripada rentang awal 32–44px pada dokumen |
| Struktur konten | Daftar terbuka dan baris bergaris; bukan kartu putih pada semua bagian | Berbeda dari contoh kartu dalam perencanaan; perbedaan bukan otomatis bug |
| Responsif | Menu desktop mulai 1024px; menu details di bawahnya; gutter 24px dan 20px pada ponsel | Pendekatan mobile-first nyata |

Sumber: `resources/css/home.css`, `resources/views/layouts/public.blade.php`, partial header/footer, dan screenshot. Kesamaan token tidak berarti seluruh kombinasi sudah memenuhi WCAG 2.2 AA.

### Aset

Tiga foto lokal: `public/images/demo/aksi-pesisir.jpg`, `ruang-belajar.jpg`, dan `pesisir.jpg`. Ketiganya merupakan ilustrasi Unsplash, bukan bukti kegiatan, tempat, orang, atau afiliasi Airlow. Kredit ada di footer. Dua font lokal memiliki file lisensi OFL. Tidak ditemukan dokumentasi organisasi resmi yang dikonfirmasi atau video dalam halaman yang diaudit. Tidak menambahkan foto, mengunduh aset, atau mengklaim lisensi baru dalam audit.

## 2. Arsitektur informasi dan fungsi nyata

| Area | Tersedia sekarang | Batas |
|---|---|---|
| `/` → `home` | Pengenalan, tautan profil, tiga agenda, pengumuman, dua cerita, dua album | Fixture presentasi |
| `/tentang` → `about` | Pengenalan, sejarah contoh, visi/misi, kepengurusan, bidang, program | Satu halaman dengan anchor; bukan modul CMS |
| `/kegiatan` → `activities` | Daftar/kalender, bulan, kategori, tanggal terpilih, rincian | Jadwal fixture; bukan pendaftaran |
| `/kabar` → `news.index` | Berita/pengumuman dengan kategori | Data dari `resources/data/posts.php` |
| `/kabar/{slug}` → `news.show` | Artikel detail | Bukan workflow penyuntingan/penerbitan |
| `/galeri` → `gallery.index` | Album dengan kategori | Sampul dari aset ilustrasi |
| `/galeri/{slug}` → `gallery.show` | Foto dan lightbox; fallback membuka foto langsung | Bukan upload/media privat |
| `/login` → `login` | Form login internal | Tidak ada registrasi publik |
| `/dashboard` → `dashboard` | Login dan izin dashboard diwajibkan | Ringkasan/tugas memakai data simulasi |
| `/dashboard/pengguna` dan turunannya | Index/create/store/edit/update/status akun Pengurus | Admin, middleware dan policy; bukan data fixture publik |

Tidak ada rute mandiri `/pengurus`, `/program-kerja`, atau `/pengumuman` pada daftar runtime. Kepengurusan/program berada di `/tentang`; pengumuman berada di `/kabar`. CRUD konten, upload, persetujuan, penerbitan, dan pengelolaan anggota yang ada di PRD belum menjadi fungsi aktif hanya karena tampilannya disebut dalam dokumen.

Navigasi desktop: Beranda, Tentang, Kegiatan, Kabar, Galeri, Masuk pengurus. Navigasi seluler juga memiliki Tentang komunitas, Kegiatan mendatang, Pengumuman, dan Informasi kontak. Label yang berbeda ini dicatat sebagai baseline, tidak diganti dalam audit.

## 3. Pengukuran awal

Angka FAIL/WARN adalah jumlah kelompok temuan deduplikasi antarviewport dari inspector, bukan jumlah elemen rusak atau skor aksesibilitas.

| Halaman | FAIL | WARN | Foto | Temuan utama |
|---|---:|---:|---:|---|
| Beranda | 7 | 3 | 3 | 12 garis desktop, pembuka kurang dominan, ukuran font terlalu beragam, tanpa motion |
| Tentang | 4 | 5 | 0 | 25 garis desktop, komposisi teks berulang, pernyataan visi 5 baris di tablet |
| Kegiatan | 5 | 2 | 0 | Garis pemisah, pembuka panjang sebelum agenda di ponsel, tanpa motion |
| Kabar | 5 | 2 | 2 | Label di atas judul, garis, pembuka/disclaimer mengambil banyak layar ponsel |
| Galeri | 5 | 2 | 3 | Label di atas judul, garis, pengantar panjang menunda album |

Beranda: tinggi 3.502px pada desktop, 3.984px tablet, dan 5.000px ponsel. Inspector menghitung 11/10/11 ukuran font. H1 tetap dua baris di ketiga ukuran. Desktop body 18px, leading 1,6; kontras body terukur 7,2:1. Teks sekunder mendominasi sekitar 67% sampel warna teks desktop; kesannya redup walaupun angka kontras itu sendiri bukan kegagalan.

### Temuan yang perlu interpretasi

- `numbering` pada angka 07 adalah tanggal `<time>`, bukan nomor urutan dekoratif. Tanggal harus dipertahankan, bukan dihapus demi alat.
- `eyebrow` seluler yang menghubungkan periode agenda dengan 07 berasal dari salah pengenalan tanggal sebagai heading. Berbeda dengan label kategori di atas judul Kabar/Galeri yang benar-benar terlihat.
- `icon-cards` pada agenda tidak membuktikan adanya kartu fitur berikon. Screenshot menunjukkan baris agenda dengan ikon waktu/lokasi. Evaluasi komposisinya, bukan menghapus informasi waktu/lokasi.
- Lint CSS: 32 FAIL (29 hairline dan 3 shadow) serta 1 WARN font Montserrat. Hitungan mencakup seluruh CSS bersama, termasuk aturan yang tidak tampil pada beranda. Dua shadow berupa inset kalender untuk outline/fokus; satu milik menu yang benar-benar mengambang. Tidak sama dengan tiga bayangan dekoratif pada elemen diam.
- Montserrat adalah identitas yang diminta dipertahankan; WARN font tidak menjadi izin mengganti font.
- Minimum empat foto dan delapan elemen bergerak adalah standar tasteskill, bukan kebutuhan fungsional atau target WCAG. Saat ini standar itu belum dipenuhi. Pemenuhannya tidak boleh memakai foto berulang tanpa fungsi, mengarang dokumentasi, atau menghilangkan reduced motion.

## 4. Kritik visual beranda

ROUND 0

Seen in one second: nama Airlow dan foto relawan; pola split pembuka yang sangat familiar.

Idea (one sentence): belum terlihat gagasan visual yang khusus milik Airlow; nama dapat diganti tanpa mengubah komposisinya.

Live thing: rincian agenda dapat dibuka; belum menjadi interaksi khas yang menguatkan pengenalan organisasi.

Layout words by section: hero=split / tentang=split / agenda=list / pengumuman=text / kabar=split-list / galeri=grid / footer=columns.

Scores: design 5.5 · usability 7.5 · creativity 4 · content 6 → overall 5.9.

Caps applied: FAIL inspector membatasi overall ke 6; kurang dari empat foto membatasi design ke 6.5; gagasan yang dapat dipakai organisasi lain membatasi creativity ke 6. Ini penilaian baseline beranda, bukan sertifikasi atau skor seluruh situs.

Top three problems (most visible first), each with the screenshot it shows in and the fix:

1. `before/desktop-fold.jpg` dan `mobile-fold.jpg`: pembuka menyebut struktur website, bukan memberi gambaran organisasi yang spesifik. Pertajam pengenalan dari materi yang benar-benar dikonfirmasi; gunakan identitas Airlow sebagai pusat komposisi. Jangan mengisi kekosongan fakta dengan slogan baru.
2. `before/desktop-page-01.jpg`: bagian tengah menyusut menjadi teks kecil, garis, dan tautan dengan bobot yang hampir sama. Beri tiap bagian tugas serta hierarki berbeda; pakai skala dan bidang warna untuk pemisahan, bukan menghapus garis lalu meninggalkan halaman kosong.
3. `before/tablet-page-01.jpg` dan `mobile-page-01.jpg`: stok foto dan pernyataan umum belum menambah kekhasan. Tempatkan ilustrasi sesuai perannya, dan tentukan kebutuhan aset nyata sebelum implementasi. Materi contoh tetap diberi konteks simulasi.

### Halaman pendamping

`before-about/tablet-page-01.jpg`: visi contoh dipasang sebagai pernyataan besar di kolom sempit hingga lima baris; halaman profil didominasi blok teks/garis tanpa variasi visual yang membantu membedakan sejarah, visi, dan struktur.

`before-activities/mobile-fold.jpg`: sebelum daftar, layar dipakai breadcrumb, judul, pengantar, disclaimer, bulan, navigasi bulan, lalu filter. Tugas mencari kegiatan tertunda; informasi waktu dan filter tetap penting dan perlu dipertahankan.

`before-news/mobile-fold.jpg` dan `before-gallery/mobile-fold.jpg`: disclaimer panjang serta kontrol mendahului materi utama. Status simulasi harus tetap jelas, tetapi komposisinya bisa lebih efisien tanpa mengganti teks legal/prototype tanpa persetujuan.

## 5. Yang dipertahankan

- Pengenalan organisasi sebelum agenda, sesuai pilihan pengguna.
- Nama/placeholder AM Airlow, warna dan dua font yang sudah digunakan.
- Banner prototype yang jelas dan kejujuran ilustrasi.
- Link nyata ke profil/pengurus/program, kategori berita/album, daftar/kalender, dan detail.
- WIT, tanggal lengkap, alt text, ukuran gambar, loading prioritas/lazy, semantik heading, skip link, dan fokus terlihat.
- Menu native details, penutupan Escape/fokus keluar dari kode JS, fallback link album tanpa JS, serta aturan reduced motion. Perilaku keyboard manual belum diuji ulang di browser dalam audit ini.
- Backend, akun, database, izin, stack, dan dependency.

## 6. SEO dan preservation baseline

Tujuh URL publik yang diuji memakai `noindex, nofollow`. Tidak ada usulan mengubahnya. Data peringkat/Search Console: tidak tersedia.

Judul baseline: Beranda `Angkatan Muda Airlow — Kebersamaan dalam tindakan`; Tentang `Profil Organisasi — Angkatan Muda Airlow`; Kegiatan `Kegiatan & Kalender — Angkatan Muda Airlow`; Kabar `Berita & Pengumuman — Angkatan Muda Airlow`; Galeri `Galeri Foto — Angkatan Muda Airlow`. Judul detail memakai judul konten. Description per halaman tersimpan dalam template; tidak diedit.

Anchor beranda yang harus dipertahankan mencakup `beranda`, `konten`, `tentang`, `kegiatan`, `agenda-1` hingga `agenda-3`, `pengumuman`, `kabar`, `galeri`, dan `kontak`, beserta heading IDs. Profil mencakup `pengenalan`, `sejarah`, `visi-misi`, `kepengurusan`, `bidang`, dan `program`. Baseline ID lengkap untuk tujuh halaman ada di `public-baseline.json`.

Field kegiatan: `tampilan`, `bulan`, `kategori`; URL kalender juga memakai `tanggal`. Kabar/galeri memakai query `kategori`. Login memakai `email`, `password`, serta CSRF tersembunyi; ini hanya dibaca dari kode, login tidak dikirim. Nama rute dan middleware dicatat dari runtime.

Perubahan URL/rute, label navigasi, field, anchor, metadata, dan aturan indeksasi pada tahap audit: **tidak ada**.

## 7. Pemeriksaan tambahan dan batas audit

- Em-dash: 8 pada seluruh teks HTML beranda yang diparse, termasuk title dan isi disclosure yang belum dibuka. Ini baseline mentah, bukan delapan dash yang sekaligus terlihat pada layar. Banner/judul dan penanda lokasi menyumbang sebagian; jangan mengganti teks prototype/legal otomatis.
- `pre-flight` bukan nama script tersendiri pada versi ini. Script yang tersedia adalah draw, assets, lint, inspect, dan scenes. Tidak mengklaim telah menjalankan pemeriksaan yang tidak ada.
- Tidak ada direction draw pada tahap ini; audit harus disetujui terlebih dahulu. Seed/arah belum dipilih.
- Tidak ada scroll scene di implementasi yang diaudit, sehingga pemeriksaan scenes belum relevan.
- Tidak melakukan audit visual detail artikel/album, dashboard, autentikasi, screen reader, seluruh keadaan error/empty, atau seluruh kombinasi filter. Detail publik diperiksa melalui HTTP, kode, dan suite publik.
- Tidak mengklaim seluruh link telah diklik, seluruh form disubmit, atau WCAG 2.2 AA sudah tercapai.
- FAIL yang tercatat adalah baseline, belum diperbaiki karena gerbang persetujuan pengguna melarang implementasi saat ini.

## 8. Rekomendasi untuk diputuskan setelah audit

Lebih tepat melakukan **redesign komposisi dengan brand dipertahankan**, dimulai dari beranda. Penyebab rasa generik ada pada gagasan dan susunan, bukan sekadar radius atau jarak. Nama, warna, font, fakta produk, dan perilaku tetap menjadi batas. Arah komposisi perlu dideklarasikan/didealkan dengan tasteskill setelah audit disetujui, lalu disetujui lagi sebelum kode diedit.

Urutan dampak: (1) pembuka dan pengenalan yang lebih khusus, (2) skala serta komposisi bagian yang berbeda dan berisi, (3) aset jujur dan satu interaksi bermakna dari materi yang tersedia. Pengecualian terhadap radius/garis/aksen judul dan aturan art direction lain belum disetujui.

Status: menunggu persetujuan audit. Tahap deklarasi arah dan implementasi belum dimulai.
