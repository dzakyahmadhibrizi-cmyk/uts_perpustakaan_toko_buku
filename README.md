# uts_perpustakaan_toko_buku

# WANWEN BOOKHOUSE

Aplikasi web front-end sederhana untuk pemesanan buku pada toko online. Dibuat sebagai **Tugas UTS Pemrograman Web**.

Seluruh data (pengguna, katalog buku, dan data pengiriman) tidak diambil dari server atau database, tetapi dari variabel JavaScript pada file terpisah `js/data.js` dalam format Array JSON. Tema visual yang dipilih adalah dunia **Teyvat (Genshin Impact)**: langit malam, bulan, pulau melayang, dan ikon tujuh elemen. Semuanya dibuat dengan HTML, CSS, SVG, dan JavaScript, tanpa gambar resmi game.

## Indikator yang Dipenuhi

- Struktur HTML yang semantik dan valid (`header`, `nav`, `main`, `section`, `footer`, `form`, `label`, `table`).
- Pengelolaan gaya antarmuka dengan CSS eksternal, internal (variabel CSS), dan inline pada elemen tertentu.
- JavaScript untuk manipulasi DOM, validasi form, manipulasi data tabel, dan interaksi UI (alert, modal box, toast, progress bar).

## Struktur Folder

```text
tugas-uts-web1/
├── index.html        (halaman login)
├── login.html        (mengarahkan ke index.html)
├── dashboard.html    (menu utama)
├── stok.html         (informasi stok / katalog)
├── checkout.html     (pemesanan)
├── tracking.html     (informasi pengiriman)
├── css/
│   ├── style.css          (gaya dasar semua halaman)
│   ├── login-genshin.css  (tema halaman login)
│   ├── tema-dalam.css     (tema halaman dalam)
│   └── scene.css          (animasi pemandangan)
├── js/
│   ├── script.js          (logika semua halaman)
│   ├── data.js            (data pengguna, katalog, tracking)
│   ├── tema.js            (slot gambar/GIF tambahan lewat link)
│   └── scene.js           (menyisipkan pemandangan Teyvat)
├── img/                   (cover buku)
└── docs/screenshots/      (tangkapan layar untuk README ini)
```

Pemisahan file dibuat modular: satu CSS dasar untuk semua halaman, CSS tema terpisah per area, satu file data, satu file logika utama, dan file kecil khusus untuk tema dan pemandangan.

## Cara Menjalankan

1. Ekstrak proyek.
2. Buka `index.html` dengan browser (klik dua kali).
3. Login memakai akun contoh:

   | Email | Password | Role |
   |---|---|---|
   | rina@gmail.com | rina123 | User |
   | agus@gmail.com | agus123 | User |
   | siti@gmail.com | siti123 | Admin |

4. Pastikan folder `css`, `js`, dan `img` tetap berdampingan dengan file HTML.

## Alur Berpikir dan Sistematika Pengerjaan

1. Membaca soal dan menurunkannya menjadi daftar halaman, fitur, dan kriteria penilaian.
2. Menyusun kerangka HTML semantik tiap halaman terlebih dahulu (tanpa gaya) agar struktur valid dan lengkap.
3. Membuat data dummy pada `data.js`, lalu menentukan variabel yang dipakai tiap halaman (`dataPengguna`, `dataKatalogBuku`, `dataTracking`).
4. Mendesain CSS: variabel warna di `:root`, komponen yang dipakai ulang (card, tombol, tabel, modal), lalu tema Teyvat.
5. Menulis JavaScript per halaman dalam satu `script.js`; halaman dikenali lewat `id` pada elemen `body`.
6. Menambahkan validasi dan umpan balik error (pesan di bawah input, alert, toast).
7. Menambahkan kreativitas: tema Teyvat dan pemandangan animasi.
8. Menguji tiap alur dan memperbaiki bug yang ditemukan.

## Penjelasan Halaman dan Tangkapan Layar

### 1. Halaman Login (`index.html`)

Berisi input email dan password serta tombol **Login**. Email dan password diperiksa terhadap `dataPengguna`. Jika kosong, muncul pesan merah di bawah kolom. Jika tidak cocok, muncul alert: *"Email/password yang anda masukkan salah"* (dialog bawaan browser, sehingga tidak tampak pada tangkapan layar). Jika berhasil, data pengguna disimpan di `localStorage` dan halaman berpindah ke dashboard.

![Tampilan halaman login](docs/screenshots/01_login.png)
*Gambar 1. Tampilan halaman login*

![Validasi form login kosong](docs/screenshots/02_login_validasi.png)
*Gambar 2. Validasi saat form login dikirim dalam keadaan kosong*

Tombol **Lupa Password** dan **Daftar** tampil dalam bentuk modal box. Modal Lupa Password memeriksa apakah email terdaftar. Modal Daftar memvalidasi nama, email, panjang password (minimal 6 karakter), mencegah email ganda, lalu menambahkan pengguna baru ke `dataPengguna`.

![Modal Lupa Password](docs/screenshots/03_modal_lupa.png)
*Gambar 3. Modal box Lupa Password*

![Modal Daftar Akun](docs/screenshots/04_modal_daftar.png)
*Gambar 4. Modal box Daftar Akun*

### 2. Dashboard (`dashboard.html`)

Menampilkan greeting berdasarkan waktu lokal memakai `new Date().getHours()`: pagi (sebelum pukul 11), siang (11 sampai 14), sore (15 sampai 17), dan malam (mulai pukul 18), beserta jam yang diperbarui tiap detik. Ada empat tombol menu: **Informasi Stok/Katalog**, **Tracking Pengiriman**, **Laporan Pemesanan**, dan **History Transaksi**. Halaman hanya bisa dibuka setelah login; jika belum, pengguna dialihkan ke halaman login.

![Dashboard](docs/screenshots/05_dashboard.png)
*Gambar 5. Dashboard dengan greeting, menu navigasi, dan pemandangan Teyvat*

![History Transaksi](docs/screenshots/06_history.png)
*Gambar 6. History Transaksi dalam modal box (kosong sebelum ada pesanan)*

### 3. Informasi Stok / Katalog (`stok.html`)

Tabel dibuat secara dinamis dari array `dataKatalogBuku` menggunakan JavaScript DOM (`createElement` dan `innerHTML`). Setiap baris menampilkan cover, kode, nama, jenis, edisi, stok, dan harga. Stok di bawah 200 diberi warna merah. Form **Tambah Stok Baru** memvalidasi semua kolom (kode wajib dan unik, edisi minimal 1, harga lebih dari 0) lalu menambahkan baris baru ke tabel. Setiap baris juga bisa dihapus.

![Tabel katalog](docs/screenshots/07_stok.png)
*Gambar 7. Tabel katalog yang dibuat dinamis dari `data.js`*

![Baris stok baru ditambahkan](docs/screenshots/08_stok_tambah.png)
*Gambar 8. Baris stok baru (Pemasaran Digital) berhasil ditambahkan*

### 4. Halaman Pemesanan (`checkout.html`)

Pengguna memilih buku dan jumlah, lalu menambahkannya ke keranjang. Jumlah dapat diubah langsung pada tabel, baris dapat dihapus, dan total dihitung otomatis. Form data pemesan dan pembayaran divalidasi (nama, format email, telepon 9 sampai 14 digit, alamat minimal 10 karakter, metode pembayaran, dan keranjang tidak boleh kosong). Setelah berhasil, sistem membuat Nomor DO, menyimpan pesanan ke `localStorage`, dan menampilkannya dalam modal.

![Keranjang pemesanan](docs/screenshots/09_checkout_keranjang.png)
*Gambar 9. Keranjang berisi pesanan yang dapat diubah dan dihapus*

![Validasi form pemesanan](docs/screenshots/10_checkout_validasi.png)
*Gambar 10. Umpan balik error saat form dikirim dengan data belum lengkap*

![Pesanan berhasil](docs/screenshots/11_checkout_sukses.png)
*Gambar 11. Modal pesanan berhasil beserta Nomor DO*

### 5. Informasi Pengiriman (`tracking.html`)

Pengguna memasukkan Nomor Delivery Order lalu menekan **Cari**. Jika ditemukan di `dataTracking` (atau di pesanan yang baru dibuat), halaman menampilkan nama pemesan, status pengiriman dengan lencana dan progress bar berwarna, detail ekspedisi, tanggal kirim, jenis paket, total pembayaran, serta riwayat perjalanan dalam bentuk timeline. Jika tidak ditemukan, muncul alert *"Nomor DO tidak ditemukan"*. Nomor DO contoh: `20230012` dan `20230013`.

![Form pencarian tracking](docs/screenshots/12_tracking_kosong.png)
*Gambar 12. Form pencarian Nomor DO*

![Hasil tracking](docs/screenshots/13_tracking_hasil.png)
*Gambar 13. Hasil pencarian: nama, status, progress bar, detail, dan timeline*

![Nomor DO tidak ditemukan](docs/screenshots/14_tracking_tidak_ada.png)
*Gambar 14. Pesan error untuk Nomor DO yang tidak valid atau tidak ditemukan*

## Fitur Kreativitas Tambahan

- **Tema Teyvat:** langit malam, bulan bercahaya, pulau melayang, awan, angin, dan daun berguguran dalam SVG animasi (`scene.js` dan `scene.css`) pada halaman dalam.
- **Ikon tujuh elemen** (Anemo, Geo, Electro, Dendro, Hydro, Pyro, Cryo) pada halaman login, dibuat dengan CSS.
- **Slot gambar/GIF lewat link** pada `js/tema.js`, dengan cadangan otomatis bila link gagal dimuat.
- **Aksesibilitas gerak:** animasi dimatikan bila pengguna mengaktifkan pengaturan *kurangi gerakan* (`prefers-reduced-motion`).

## Kesesuaian dengan Kriteria Penilaian

| Kriteria | Penerapan |
|---|---|
| Struktur HTML semantik | `header`, `nav`, `main`, `section`, `footer`, `form` dengan `label`, `table` dengan `thead`/`tbody`, atribut `lang` dan `alt` |
| Desain CSS | File eksternal, variabel `:root`, grid dan flexbox, responsif, tema gelap bernuansa Teyvat |
| JavaScript DOM | Tabel dinamis, keranjang, timeline, modal, greeting waktu |
| Validasi form dan alert | Pesan error di bawah input, alert, toast, modal konfirmasi |
| Modularitas file | CSS, JS, data, dan gambar dipisah dalam folder sesuai struktur soal |
| Kreativitas | Tema Teyvat, SVG animasi, `localStorage` untuk keranjang dan riwayat |
