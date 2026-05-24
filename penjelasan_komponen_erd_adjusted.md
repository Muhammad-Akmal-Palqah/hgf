Penjelasan Komponen Entity Relationship Diagram (ERD)

Bagian ini mendeskripsikan seluruh komponen, atribut, dan hubungan (relasi) antar-entitas yang wajib digambar dalam diagram ERD sistem R.R Hijab untuk memenuhi kebutuhan penyimpanan data pada database MySQL, diselaraskan dengan aturan batas waktu otomatisasi sistem.

Entitas Data Admin

Entitas ini digunakan untuk menyimpan data akun pengelola sistem yang diakses melalui Sistem Berbasis Web.

- Atribut ID Admin: Berperan sebagai Primary Key (kunci utama) berupa angka unik yang bertambah otomatis untuk membedakan setiap akun admin.
- Atribut Username: Berupa teks singkat untuk identitas login dan bersifat unik tidak boleh ada yang sama.
- Atribut Password: Berupa teks rahasia yang sudah disamarkan menggunakan enkripsi keamanan.

Hubungan Relasi Admin: Seorang Admin dapat mengelola banyak data produk di dalam sistem (Hubungan Satu ke Banyak / One to Many).

---

Entitas Data Produk

Entitas ini digunakan untuk menyimpan seluruh informasi katalog jilbab dan aksesoris yang bersumber dari supplier.

- Atribut ID Produk: Berperan sebagai Primary Key (kunci utama) berupa kode unik untuk penanda setiap jenis jilbab.
- Atribut Nama Produk: Berupa teks untuk menampilkan nama hijab di halaman utama Web dan Aplikasi Mobile.
- Atribut Deskripsi Produk: Berupa teks panjang yang menjelaskan detail bahan, ukuran, dan warna hijab.
- Atribut Kategori: Berupa teks untuk mengelompokkan jenis produk seperti Pashmina atau Hijab Instan.
- Atribut Harga: Berupa angka positif untuk nominal harga jual.
- Atribut Tautan Gambar: Berupa teks alamat URL yang mengarah ke file foto produk di server supplier.

Hubungan Relasi Produk: Satu produk dapat dipilih di dalam banyak data pesanan pelanggan (Hubungan Satu ke Banyak / One to Many).

---

Entitas Data Pesanan

Entitas ini digunakan untuk mencatat rekam transaksi pembelian dari aplikasi mobile Flutter sebelum divalidasi oleh admin web.

- Atribut ID Pesanan: Berperan sebagai Primary Key (kunci utama) berupa nomor invoice unik untuk tiap transaksi belanja.
- Atribut Nama Pelanggan: Berupa teks nama lengkap pihak pembeli.
- Atribut Nomor WhatsApp: Berupa teks atau angka nomor kontak aktif pembeli.
- Atribut Status Pesanan: Berupa teks status kondisi transaksi saat ini yang berisi Menunggu Pembayaran, Diproses, atau Dibatalkan Sistem setelah melewati batas waktu dua puluh empat jam.
- Atribut Waktu Pembuatan (Timestamp): Berupa data tanggal dan waktu saat pelanggan menekan tombol order di aplikasi mobile Flutter. Atribut ini digunakan oleh web server sebagai acuan hitung mundur dua puluh empat jam sebelum pesanan otomatis dianggap hangus.
- Atribut ID Produk: Berperan sebagai Foreign Key (kunci tamu) yang menghubungkan data pesanan dengan asal produk yang dibeli.

Hubungan Relasi Pesanan: Satu pesanan dapat menerima satu data ulasan atau masukan purna jual setelah transaksi dinyatakan selesai (Hubungan Satu ke Satu / One to One).

---

Entitas Data Feedback

Entitas ini digunakan pada fitur purna jual untuk menampung ulasan dari pihak pembeli aplikasi mobile Flutter setelah barang sampai.

- Atribut ID Feedback: Berperan sebagai Primary Key (kunci utama) berupa angka unik penanda ulasan yang bertambah otomatis.
- Atribut Nama Pengirim: Berupa teks nama pelanggan yang memberikan komentar.
- Atribut Isi Komentar: Berupa teks ulasan mengenai kualitas pelayanan atau produk hijab.
- Atribut ID Pesanan: Berperan sebagai Foreign Key (kunci tamu) untuk memastikan ulasan yang dikirim tangan pertama valid berdasarkan transaksi asli yang pernah terjadi di database.
