# Usulan arah beranda Airlow

Status: audit disetujui; arah ini menunggu persetujuan. Tidak ada kode aplikasi yang diubah.

## Mode dan batas scope

Redesign komposisi dengan brand dipertahankan. Implementasi pertama hanya beranda `/`. Bila header/footer memerlukan perlakuan berbeda, gunakan scope beranda agar halaman publik lain dan dashboard tidak ikut berubah tanpa persetujuan. Tidak memigrasi stack, menambah dependency, mengubah backend, atau menyentuh database.

## Inventaris subjek

1. Nama kerja Angkatan Muda Airlow; arti atau riwayat nama belum dikonfirmasi.
2. Placeholder AM dan wordmark Airlow, bukan lambang resmi.
3. Bahasa Indonesia dan waktu kegiatan WIT.
4. Prioritas pembaca: mengenal organisasi sebelum membaca agenda.
5. Profil tersedia di `/tentang` dengan pengenalan dan sejarah simulasi.
6. Susunan pengurus berupa jabatan serta nama contoh; bukan foto atau identitas anggota nyata.
7. Program contoh: Temu Muda & Refleksi, Ruang Belajar Kreatif, Aksi Bersih Pesisir.
8. Tiga tanggal agenda beranda: 7, 14, dan 21 November 2026, seluruhnya simulasi.
9. Dua cerita contoh menghubungkan kegiatan pesisir dan ruang belajar.
10. Tiga foto ilustrasi lokal, tanpa dokumentasi atau footage Airlow yang dikonfirmasi.
11. Batas produk yang nyata: bukan situs resmi, tanpa pendaftaran publik dan tanpa workflow penerbitan aktif.

Inventaris ini memberi materi konkret, tetapi belum membuktikan keunikan budaya, lokasi, atau sejarah organisasi. Desain tidak boleh mengarangnya agar konsep terlihat lebih khas.

## Argumen halaman

| Urutan | Hal yang dijelaskan | Materi pendukung |
|---|---|---|
| Pembuka | Ini Angkatan Muda Airlow, dalam prototype pengenalan organisasi | Nama, konteks simulasi, tombol Baca profil Airlow |
| Tentang | Pembaca dapat mengenal profil, pengurus, dan program | Tiga tautan ke anchor profil yang sudah tersedia |
| Agenda | Ada contoh kegiatan yang dapat diperiksa tanggal dan rinciannya | Tiga agenda lengkap dengan waktu, tempat, dan rincian |
| Kabar/pengumuman | Pembaca dapat membuka cerita serta pengumuman yang tersedia | Dua artikel dan pengumuman yang sama; tautan tetap |
| Galeri | Ada album ilustrasi untuk melengkapi pengenalan | Album dan kredit yang sudah ada; aset tambahan harus jujur |
| Penutup | Ini prototype; kontak resmi belum ditetapkan | Teks legal/prototype, kredit, dan link yang sudah tersedia |

Ini urutan baca, bukan izin mengganti ID/anchor atau menghilangkan isi yang ada.

## Hasil draw dan pilihan

Sektor nonprofit; `--keep palette,type`; roles about, list, work, gallery, footer. Tiga opsi awal: editorial-report, borrowed-category, uneven-photographs.

Dipilih **editorial-report / The printed annual**, seed **1757561471**. Bentuk buletin mengutamakan pengenalan serta program, sesuai pilihan pengguna. Borrowed-category menambah analogi yang belum berasal dari fakta Airlow; uneven-photographs bergantung pada banyak foto yang belum tersedia.

Ide: **Nama Airlow, profil, dan agenda contoh November menjadi isi sampul serta rubrik sebuah buletin komunitas.** Ini bukan laporan tahunan resmi, bukan klaim sejarah organisasi, dan bukan alasan menambah tahun edisi atau nomor bab dekoratif.

Uji pesaing: konsep buletin dapat dipakai komunitas lain. Kekhasan sementara bertumpu pada nama dan isi Airlow yang tersedia; jangan mengklaim arah ini unik secara budaya sebelum materi organisasi dikonfirmasi.

## Komposisi yang diusulkan

### Pembuka: papan sampul, bukan split hero lama

Blueprint hero akhir adalah **Two-by-two board**: susunan bidang berisi nama besar, dua ilustrasi, dan pengantar singkat dalam bidang warna. Semua bidang memiliki isi, tanpa outline, gradient, atau bayangan dekoratif. Nama Airlow menjadi pusat perhatian; nama lengkap tetap jelas melalui wordmark dan kalimat pendukung. Tombol utama tetap **Baca profil Airlow**, menuju `/tentang`; Lihat jadwal kegiatan tetap tersedia.

Pengantar harus menyatakan bahwa ini Angkatan Muda Airlow dalam prototype pengenalan organisasi. Jangan memakai slogan keberhasilan atau klaim organisasi baru. Banner **Prototype — Data simulasi** dan teks legal tetap ada. Foto bukan bukti kegiatan Airlow.

Pada ponsel papan menjadi urutan nama/pengantar/aksi lalu foto; tidak ada teks menimpa gambar atau judul. Judul dibatasi dua baris. Bentuk akhir diuji pada 1440, 768, dan 390 px, bukan diputuskan dari kode saja.

### Tentang: fakta dan pengenalan

Blueprint **Side facts, wide paragraph**: ringkasan pendek di satu sisi dan pengenalan di sisi lain. Isi menggunakan profil, kepengurusan, dan program yang tersedia. Tidak mengisi label bawaan founded/based/team size, karena fakta itu belum ada. Tautan profil/sejarah, pengurus, dan program tetap menjadi pintu utama.

### Agenda: tanggal yang dapat dipilih

Blueprint **Day tabs, banded agenda**: pilihan tanggal dan rincian kegiatan pada bidang dengan perubahan tone, bukan garis. Live thing: memilih 7, 14, atau 21 November untuk membaca agenda contoh pada tanggal itu. Label menyebut tanggal nyata, bukan angka dekoratif. Waktu WIT, tempat simulasi, dan rincian tetap utuh. Tanpa JavaScript semua agenda tetap terbaca dan anchor tetap valid. Ini enhancement presentasi pada beranda, bukan pendaftaran atau pengelolaan agenda baru.

### Kabar: indeks pendek dengan preview

Blueprint **Quiet ledger, side preview**: dua cerita yang ada menjadi indeks bacaan dengan satu area gambar pendamping. Tidak menambahkan proyek atau artikel fiktif demi kepadatan layout. Judul, tanggal, excerpt, dan tujuan tautan tetap. Pengumuman tetap tersedia dan mendapat penempatan yang jelas.

### Galeri dan penutup

Blueprint **Photo tiles with label strips**: album tampil seperti lembar foto dengan caption yang menyatu, bukan masonry dua puluh gambar. Tidak menambah album baru atau menggandakan foto hanya untuk mengejar hitungan inspector.

Footer memakai **Name first, places under it**, dengan nama kembali dominan dan informasi nyata di bawahnya. Tidak membuat alamat, telepon, atau kontak baru. Legal dan kredit tetap lengkap; teks nama tidak dipotong hingga sulit dibaca.

## Brand dan pengecualian yang diminta

Dipertahankan: primary `#184A9C`, accent `#EF813F`, canvas `#F7F9FC`, ink `#17263D`; Montserrat untuk heading dan Source Sans 3 untuk teks; placeholder AM dan wordmark; bahasa Indonesia; status prototype.

Perubahan visual yang memerlukan persetujuan arah ini:

- Nama pada judul memakai satu warna, tanpa kata Airlow diberi warna khusus. Wordmark/logo tetap seperti semula.
- Ukuran display diperbesar sesuai komposisi dan batas dua baris; skala pendukung disederhanakan menuju lima tingkat.
- Bidang dan foto memakai sudut persegi; tombol CTA beranda juga persegi. Ini pengecualian dari radius sementara 8/12/16px, dibatasi pada beranda. Form di halaman lain tetap.
- Garis pemisah dekoratif pada beranda diganti ruang, tone, atau skala. Focus ring dan kebutuhan kontrol tetap dipertahankan.
- Teks isi utama memakai ink penuh; muted dibatasi pada metadata/credit.

Tidak mengubah token warna/font global untuk mengikuti palette/type baru.

## Aset dan motion

Tiga foto lama dapat dipakai sebagai ilustrasi dengan kredit. Sebelum memenuhi minimum empat gambar tasteskill, cari aset tambahan yang relevan dan periksa sumber/lisensinya. Jangan menyimpulkan lokasi Airlow dari foto pesisir; lokasi organisasi belum dikonfirmasi. Bila tidak ada aset jujur, laporkan gap, bukan memasang gambar palsu atau menganggap gate lulus.

Signature motion yang didealkan: **Slow crossfade** pada foto ilustrasi. Perubahan harus tenang, dapat dihentikan, dan tidak memindahkan konten saat dibaca. Gerak pendukung hanya transform/opacity; konten terlihat tanpa script; prefers-reduced-motion menampilkan gambar statis tanpa travel. Video hanya jika ada clip relevan yang lisensinya jelas; bukan kewajiban mengarang footage organisasi.

## Empat redraw dan alasan

1. Hero: View with two cards in the corner → Two-by-two board. Hero awal mengandalkan foto/film utama yang bisa disalahpahami sebagai dokumentasi Airlow dan dua kartu visual tambahan. Tidak ada dokumentasi utama yang dikonfirmasi; nama serta pengantar perlu menjadi materi utama.
2. About: Wide photo, colour tile, facts → Side facts, wide paragraph. Blueprint awal meminta peta/floor plan, lokasi, altitude/distance/season yang tidak tersedia. Blueprint pengganti memakai materi profil yang sudah ada.
3. Work: Staggered tiles, empty cells → Quiet ledger, side preview. Blueprint awal mengasumsikan delapan proyek visual; beranda memiliki dua cerita. Tidak menambah proyek untuk mengisi grid.
4. Gallery: Dense masonry sheet → Photo tiles with label strips. Blueprint awal membutuhkan sekitar dua puluh gambar; tersedia tiga foto dan dua pintu album di beranda. Tidak menciptakan kepadatan dengan pengulangan tanpa fungsi.

Blueprint lower priority diterjemahkan melalui aturan arah dan house rules: axis desktop tetap diulang, tetapi sisi lain selalu memuat ringkasan/gambar/tautan, bukan kekosongan. Tidak memakai print furniture seperti nomor halaman, kicker, atau garis.

## Urutan implementasi setelah persetujuan

1. Pembuka organisasi dan hierarki nama/pengantar/aksi.
2. Skala type, bidang warna, frame, serta komposisi ponsel.
3. Rubrik profil, agenda, kabar, galeri, dan penutup sesuai blueprint.
4. Aset tambahan yang jujur dan live thing agenda dengan fallback.
5. Fokus, keyboard, feedback kontrol, dan motion/reduced motion.
6. Build dan lint/inspect hasil yang disajikan, screenshot tiga lebar, kritik maksimum tiga putaran, dan tes publik yang terdampak.

## Dampak preservasi

| Hal | Usulan |
|---|---|
| URL/nama rute | Tidak berubah |
| Label navigasi | Tidak berubah, termasuk variasi desktop/seluler yang ada |
| ID/anchor | Tidak berubah; simpan seluruh baseline termasuk anchor agenda dan heading |
| Nama field/form | Tidak berubah; tidak menambah form pengumpulan data |
| Title/description/robots | Tidak berubah; `noindex, nofollow` tetap |
| Backend/role/auth | Tidak berubah |
| Perilaku | Tambahan pilihan tanggal agenda di beranda saja; rincian/fallback tetap dapat diakses |
| Copy terlihat | Pengantar dan susunan penjelasan beranda dirapikan tanpa fakta baru; nama cerita/agenda dan teks legal/prototype dipertahankan |
| Dashboard/halaman lain | Tidak direstyle pada tahap implementasi pertama |

Arah visual ini belum merupakan hasil implementasi atau janji skor. Tidak ada klaim gate lulus pada versi baru yang belum dibangun.
