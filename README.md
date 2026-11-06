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

<img width="1280" height="760" alt="01_login" src="https://github.com/user-attachments/assets/4a192b47-9a0b-46c0-ae3b-720bf152119d" />

*Gambar 1. Tampilan halaman login*

![Validasi form login kosong](<img width="1280" height="760" alt="02_login_validasi" src="https://github.com/user-attachments/assets/40aa7415-a696-48ed-89b0-964d575755ff" />
)
*Gambar 2. Validasi saat form login dikirim dalam keadaan kosong*

Tombol **Lupa Password** dan **Daftar** tampil dalam bentuk modal box. Modal Lupa Password memeriksa apakah email terdaftar. Modal Daftar memvalidasi nama, email, panjang password (minimal 6 karakter), mencegah email ganda, lalu menambahkan pengguna baru ke `dataPengguna`.

![Modal Lupa Password](<img width="1280" height="760" alt="03_modal_lupa" src="https://github.com/user-attachments/assets/6676b0f4-7932-466a-97c2-bf805844b23c" />
)
*Gambar 3. Modal box Lupa Password*

![Modal Daftar Akun](<img width="1280" height="760" alt="04_modal_daftar" src="https://github.com/user-attachments/assets/9e79970c-476e-4ca0-bffc-98e51f08168d" />
)
*Gambar 4. Modal box Daftar Akun*

### 2. Dashboard (`dashboard.html`)

Menampilkan greeting berdasarkan waktu lokal memakai `new Date().getHours()`: pagi (sebelum pukul 11), siang (11 sampai 14), sore (15 sampai 17), dan malam (mulai pukul 18), beserta jam yang diperbarui tiap detik. Ada empat tombol menu: **Informasi Stok/Katalog**, **Tracking Pengiriman**, **Laporan Pemesanan**, dan **History Transaksi**. Halaman hanya bisa dibuka setelah login; jika belum, pengguna dialihkan ke halaman login.

![Dashboard](<img width="1280" height="760" alt="05_dashboard" src="https://github.com/user-attachments/assets/b282da5e-ccca-4010-985e-8b7319c9de7e" />
)
*Gambar 5. Dashboard dengan greeting, menu navigasi, dan pemandangan Teyvat*

![History Transaksi](<img width="1280" height="760" alt="06_history" src="https://github.com/user-attachments/assets/1d61b08a-b190-4df2-b686-a8444a15698e" />
)
*Gambar 6. History Transaksi dalam modal box (kosong sebelum ada pesanan)*

### 3. Informasi Stok / Katalog (`stok.html`)

Tabel dibuat secara dinamis dari array `dataKatalogBuku` menggunakan JavaScript DOM (`createElement` dan `innerHTML`). Setiap baris menampilkan cover, kode, nama, jenis, edisi, stok, dan harga. Stok di bawah 200 diberi warna merah. Form **Tambah Stok Baru** memvalidasi semua kolom (kode wajib dan unik, edisi minimal 1, harga lebih dari 0) lalu menambahkan baris baru ke tabel. Setiap baris juga bisa dihapus.

![Tabel katalog](<img width="1280" height="760" alt="07_stok" src="https://github.com/user-attachments/assets/2973f06a-235e-44cb-8af9-6eabda3ba35b" />
)
*Gambar 7. Tabel katalog yang dibuat dinamis dari `data.js`*

![Baris stok baru ditambahkan](<img width="1280" height="1150" alt="08_stok_tambah" src="https://github.com/user-attachments/assets/20b19a26-0f22-4201-92c8-a51f8f398b08" />
)
*Gambar 8. Baris stok baru (Pemasaran Digital) berhasil ditambahkan*

### 4. Halaman Pemesanan (`checkout.html`)

Pengguna memilih buku dan jumlah, lalu menambahkannya ke keranjang. Jumlah dapat diubah langsung pada tabel, baris dapat dihapus, dan total dihitung otomatis. Form data pemesan dan pembayaran divalidasi (nama, format email, telepon 9 sampai 14 digit, alamat minimal 10 karakter, metode pembayaran, dan keranjang tidak boleh kosong). Setelah berhasil, sistem membuat Nomor DO, menyimpan pesanan ke `localStorage`, dan menampilkannya dalam modal.

![Keranjang pemesanan](<img width="1280" height="1150" alt="09_checkout_keranjang" src="https://github.com/user-attachments/assets/1d76c696-7eca-4b6d-80a4-651b14e11251" />
)
*Gambar 9. Keranjang berisi pesanan yang dapat diubah dan dihapus*

![Validasi form pemesanan](<img width="1280" height="1150" alt="10_checkout_validasi" src="https://github.com/user-attachments/assets/06a17972-fd7e-4321-9ed9-2260363a853d" />
)
*Gambar 10. Umpan balik error saat form dikirim dengan data belum lengkap*

![Pesanan berhasil](<img width="1280" height="760" alt="11_checkout_sukses" src="https://github.com/user-attachments/assets/96db0142-cf37-4baf-8597-9a16ea4f6883" />
)
*Gambar 11. Modal pesanan berhasil beserta Nomor DO*

### 5. Informasi Pengiriman (`tracking.html`)

Pengguna memasukkan Nomor Delivery Order lalu menekan **Cari**. Jika ditemukan di `dataTracking` (atau di pesanan yang baru dibuat), halaman menampilkan nama pemesan, status pengiriman dengan lencana dan progress bar berwarna, detail ekspedisi, tanggal kirim, jenis paket, total pembayaran, serta riwayat perjalanan dalam bentuk timeline. Jika tidak ditemukan, muncul alert *"Nomor DO tidak ditemukan"*. Nomor DO contoh: `20230012` dan `20230013`.

![Form pencarian tracking](<img width="1280" height="760" alt="12_tracking_kosong" src="https://github.com/user-attachments/assets/99e3f1fd-7a40-4de6-bcec-0465c268e187" />
)
*Gambar 12. Form pencarian Nomor DO*

![Hasil tracking](<img width="1280" height="1150" alt="13_tracking_hasil" src="https://github.com/user-attachments/assets/0e79a7c6-f64b-4158-921a-c49ec6a5a189" />
)
*Gambar 13. Hasil pencarian: nama, status, progress bar, detail, dan timeline*

![Nomor DO tidak ditemukan](<img width="1280" height="760" alt="14_tracking_tidak_ada" src="https://github.com/user-attachments/assets/8fde16eb-5e60-4882-b99e-c5eb61d3aee5" />
)
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
