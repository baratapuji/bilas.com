# Bilas - Landing Page Laundry Antar-Jemput

Landing page bisnis satu file (`index.html`) untuk layanan laundry kiloan antar-jemput. Dibuat sebagai tugas landing page dengan **HTML, Tailwind CSS (CDN), dan JavaScript** tanpa framework dan tanpa proses build.

## Fitur

- **Navbar sticky** dengan menu hamburger di tampilan HP.
- **Kalkulator harga interaktif** di hero: geser berat cucian, pilih layanan, lalu total harga, ongkir, dan perkiraan tanggal selesai langsung dihitung.
- **Pesan lewat WhatsApp**: hasil kalkulator dan isi formulir otomatis menjadi pesan WhatsApp.
- **Cara kerja** dalam 3 langkah.
- **Daftar harga** layanan.
- **Testimoni** pelanggan.
- **FAQ accordion** (buka-tutup dengan animasi halus).
- **Form pemesanan** dengan validasi nama dan alamat.
- **Responsif** untuk HP, tablet, dan desktop.
- **Aksesibilitas dasar**: fokus keyboard terlihat, atribut `aria-expanded`, dan animasi dimatikan untuk pengguna yang memilih *reduced motion*.

## Teknologi

| Teknologi | Kegunaan |
|---|---|
| HTML5 | Struktur halaman |
| [Tailwind CSS 3.4.17](https://tailwindcss.com) via CDN | Styling dengan utility class |
| CSS tambahan (`<style>`) | Animasi gelembung, animasi FAQ, gaya fokus |
| JavaScript (vanilla) | Menu mobile, kalkulator, FAQ, validasi form |
| Google Fonts | Bricolage Grotesque (judul) dan Figtree (isi) |

## Cara Menjalankan

1. Unduh atau salin file `index.html`.
2. Buka file tersebut di browser (klik dua kali, atau gunakan ekstensi *Live Server* di VS Code).
3. Pastikan perangkat **terhubung ke internet**, karena Tailwind dan font dimuat dari CDN.

Tidak perlu menginstal apa pun.

## Struktur File

```
.
|-- index.html    <- seluruh halaman (HTML + CSS + JS)
`-- README.md     <- dokumen ini
```

Susunan di dalam `index.html`:

| Bagian | Isi |
|---|---|
| `<head>` | Tailwind CDN, font, konfigurasi warna dan font, CSS tambahan |
| `<header>` | Navbar dan menu mobile |
| `<main>` | Hero + kalkulator, Cara kerja, Harga, Testimoni, FAQ, Form pesan |
| `<footer>` | Hak cipta (tahun otomatis) |
| `<script>` (paling bawah) | Seluruh logika JavaScript |

## Cara Mengubah Isi

### 1. Nomor WhatsApp

Cari baris ini di bagian JavaScript paling bawah:

```js
const NOMOR_WA = "6281234567890";
```

Ganti dengan nomor sendiri dalam format internasional: tanpa tanda `+` dan tanpa `0` di depan (contoh `0812...` menjadi `62812...`). Ubah juga tautan `wa.me` dan teks nomor di bagian "Siap jemput cucianmu hari ini?".

### 2. Harga layanan

Harga untuk kalkulator ada di objek `LAYANAN`:

```js
const LAYANAN = {
  reguler: { nama: "Kiloan reguler", harga: 7000,  hari: 2 },
  kilat:   { nama: "Kiloan kilat",   harga: 12000, hari: 0 },
  setrika: { nama: "Setrika saja",   harga: 5000,  hari: 1 }
};
```

- `harga` adalah harga per kg.
- `hari` adalah lama pengerjaan (0 berarti hitungan jam).

Aturan lain ada di fungsi `hitung()`: minimal tagihan **3 kg** (`Math.max(kg, 3)`) dan gratis ongkir mulai **5 kg** (`kg >= 5`). Daftar harga di bagian HTML (section `#harga`) dan label pada pilihan layanan juga perlu disesuaikan secara manual agar sama.

### 3. Warna dan font

Ubah di blok `tailwind.config` di dalam `<head>`:

```js
colors: { ink:'#0f3d4c', sea:'#1b6f82', foam:'#f2f8f7', bubble:'#bfeee5', sun:'#ffd23f', coral:'#ff6b57' }
```

Nama warna ini dipakai sebagai class di seluruh halaman, misalnya `bg-ink`, `text-sun`, `border-sea`. Mengubah nilainya otomatis mengubah seluruh tampilan.

### 4. Teks, nama bisnis, dan jenis usaha

Semua teks berada di bagian HTML dan bisa diganti langsung. Untuk mengganti jenis bisnis (misalnya kafe atau bengkel), ubah:

- Judul `<title>` dan meta description di `<head>`.
- Nama brand di navbar dan footer.
- Judul hero, section harga, testimoni, dan FAQ.
- Isi objek `LAYANAN` dan pilihan di form.

## Cara Kerja Singkat (JavaScript)

| Fungsi | Penjelasan |
|---|---|
| Menu mobile | Tombol hamburger menambah/menghapus class `hidden` pada menu |
| `hitung()` | Membaca berat dan layanan, menghitung biaya cuci, ongkir, total, dan estimasi tanggal, lalu memperbarui tampilan dan tautan WhatsApp |
| FAQ | Klik tombol menambah class `buka` pada isi jawaban dan mengubah `aria-expanded` |
| Validasi form | Nama minimal 2 huruf, alamat minimal 10 huruf; jika valid, membuka `wa.me` dengan pesan yang sudah disusun |
| `encodeURIComponent` | Mengubah teks pesan agar aman dipakai di URL |

## Catatan

- Tailwind CDN cocok untuk belajar dan prototipe. Untuk situs produksi, sebaiknya Tailwind di-*build* terlebih dahulu agar file lebih kecil dan lebih cepat.
- Versi Tailwind dikunci di `3.4.17` supaya tampilan tidak berubah jika ada pembaruan.
- Semua nama, testimoni, harga, dan nomor telepon adalah **data contoh** dan perlu diganti sebelum dipakai untuk bisnis sungguhan.

## Lisensi

Bebas dipakai dan dimodifikasi untuk keperluan belajar.
