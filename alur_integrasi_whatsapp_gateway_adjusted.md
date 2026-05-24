Merancang Alur Teknis Integrasi WhatsApp Gateway

Bagian ini menjelaskan bagaimana sistem Web dan Aplikasi Mobile Flutter terhubung dengan layanan pihak ketiga yaitu WhatsApp Gateway untuk mengirimkan notifikasi otomatis dan memfasilitasi komunikasi transaksi, dengan memperhatikan batasan jam operasional kerja.

Alur Pengiriman Notifikasi dari Sistem Web

Sisi Sistem Berbasis Web (Company Profile dan Admin Web)

- Pemicu Validasi Transaksi: Saat pengelola sistem selesai melakukan verifikasi manual terhadap bukti transfer dan mengubah status pesanan menjadi Diproses pada sistem web, aksi ini menjadi pemicu utama. Proses verifikasi manual ini hanya dilakukan pada jam kerja aktif yaitu pukul delapan pagi sampai pukul lima sore WIB.
- Pengiriman Data ke Gateway: Sistem web secara otomatis mengumpulkan data transaksi yang diperlukan dari database MySQL, seperti nama pelanggan, nomor invoice, dan nomor WhatsApp tujuan.
- Kontrol Penundaan Jam Operasional: Jika pengelola mengubah status transaksi di luar jam kerja aktif (pukul delapan pagi sampai pukul lima sore WIB), sistem web dikonfigurasi untuk menunda pengiriman data ke server gateway guna menghindari gangguan pesan otomatis di malam hari kepada pelanggan.
- Penerusan Pesan oleh Layanan Gateway: Setelah masuk dalam waktu jam operasional aktif, sistem web meneruskan data tersebut ke server penyedia layanan WhatsApp Gateway melalui koneksi internet untuk mengirimkan pesan teks resmi ke nomor pelanggan.
- Format Pesan Otomatis: Pesan yang diterima pelanggan berupa teks biasa yang berisi konfirmasi bahwa pembayaran telah divalidasi dan pesanan mereka sedang diteruskan ke pihak supplier.

Sisi Sistem Berbasis Aplikasi Mobile (Flutter)

- Pembaruan Status Real Time: Aplikasi mobile Flutter menerima pembaruan data status dari database MySQL yang telah diubah oleh sistem web, sehingga tampilan menu riwayat di HP pelanggan ikut berubah secara otomatis menjadi Diproses secara real-time.

---

Alur Komunikasi Langsung dari Aplikasi Mobile

Sisi Sistem Berbasis Aplikasi Mobile (Flutter)

- Pemicu Tombol Pesan: Ketika pelanggan selesai memilih jilbab pada aplikasi mobile Flutter dan menekan tombol konfirmasi pesanan, sistem Flutter akan memanggil fungsi pengiriman data pesanan awal ke database MySQL. Pelanggan dapat melakukan pengiriman pesanan ini kapan saja selama dua puluh empat jam penuh.
- Penanganan Peringatan Waktu: Jika pembuatan pesanan dilakukan di luar jam kerja (sebelum pukul delapan pagi atau setelah pukul lima sore WIB), aplikasi mobile Flutter akan memunculkan teks informasi pemberitahuan bahwa transaksi dicatat di database namun verifikasi baru diproses pada hari kerja berikutnya.
- Pembuatan Tautan Otomatis: Setelah nomor invoice sukses diterbitkan oleh database, aplikasi mobile Flutter menggunakan data nomor WhatsApp tujuan milik toko dan nomor invoice tersebut untuk menyusun sebuah tautan internet khusus.
- Pengalihan Aplikasi (Deep Linking): Aplikasi mobile Flutter secara otomatis mengarahkan pelanggan keluar dari aplikasi dan membuka aplikasi WhatsApp yang terpasang di HP pelanggan melalui tautan khusus yang sudah dibuat.
- Pengiriman Pesan Manual oleh Pelanggan: Aplikasi WhatsApp di HP pelanggan akan terbuka dengan ruang obrolan langsung ke nomor toko R.R Hijab, lengkap dengan draf tulisan yang berisi detail pesanan dan nomor invoice. Pelanggan hanya perlu menekan tombol kirim di WhatsApp untuk memulai percakapan.

Sisi Sistem Berbasis Web (Arsip Data)

- Pencatatan Log Transaksi: Sistem web tetap mencatat bahwa invoice tersebut telah dialihkan menuju WhatsApp, sehingga pengelola dapat memantau pesanan mana saja yang sedang dalam tahap komunikasi chat melalui halaman dashboard web.
