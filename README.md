## Judul Capstone Project

**Kasir Kilat Es Teh Keliling**

---

## Ringkasan Project

Project Kasir Kilat Es Teh Keliling bertujuan menghadirkan aplikasi pencatatan penjualan (Point-of-Sale) berbasis tap-counter yang dapat dijalankan secara offline untuk pedagang es teh keliling. Project ini sebagai solusi sederhana atas permasalahan kesulitan pedagang dalam pencatatan transaksi secara manual ketika menghadapi lonjakan pembeli dalam satu waktu. Karena secara bersamaan tangan pedagang sibuk meracik pesanan tidak sempat menghitung jumlah kemasan gelas maupun plastik yang telah terjual dan perhitungan mengandalkan daya ingat.

AI Agent IBM Bob dapat difungsikan sebagai autonomous senior frontend & mobile-first engineer yang merancang dan membangun keseluruhan aplikasi dalam format single-file (`index.html`) tanpa dependensi pustaka eksternal. Melalui instruksi terstruktur berbasis Prompt Layering, AI Agent mengimplementasikan antarmuka dua tombol transaksi utama (Gelas Rp 5.000 dan Plastik Rp 3.500), penghitung langsung di atas setiap tombol, efek suara kencringan koin sintetis berbasis, kalkulasi total kemasan dan uang masuk secara otomatis, log riwayat ketukan berstempel waktu, serta fitur ekspor laporan harian *offline* dalam format teks siap tempel dan file CSV.

---

## Problem Statement

Kondisi Saat Ini: Pedagang es teh keliling umumnya beroperasi secara mandiri di titik-titik keramaian seperti area sekolah, perkantoran, pasar, atau pinggir jalan dengan pola kedatangan pembeli yang bergelombang secara bersamaan. Pada saat antrean padat, pedagang harus melakukan banyak tugas sekaligus dalam hitungan detik—menuang minuman, mengemas ke dalam gelas atau plastik, menyerahkan pesanan, serta menerima uang tunai dan menghitung kembalian—sehingga pencatatan penjualan masih mengandalkan ingatan semata atau penghitungan sisa kemasan di akhir hari.

Dampak Apabila Tidak Ditangani: Tanpa mekanisme pencatatan yang praktis saat melayani gelombang pembeli, pedagang sangat rentan mengalami selisih hitung/human error antara jumlah uang tunai yang terkumpul dengan jumlah stok gelas maupun plastik yang berkurang. Dalam jangka pendek, pedagang tidak dapat mengetahui omzet riil harian secara pasti; dalam jangka panjang, kesalahan hitung berulang mengakibatkan kebocoran pendapatan, kesulitan mengevaluasi varian kemasan paling laris, serta terhambatnya perencanaan belanja stok bahan baku untuk hari berikutnya.

---

## Target Users

Pengguna utama solusi ini adalah pedagang keliling es teh skala usaha mikro (UMKM) yang berjualan menggunakan gerobak dorong, sepeda motor, maupun lapak portable di area publik.

Peran: Bertindak sebagai operator tunggal yang merangkap seluruh fungsi operasional sekaligus, mulai dari peracik minuman, pelayan pelanggan, kasir transaksi tunai, hingga pencatat pembukuan harian.

Kebutuhan Utama:
1. Mekanisme pencatatan penjualan instan hanya dengan satu sentuhan ibu jari (single-tap) tanpa perlu mengetik angka atau berpindah layar.
2. Umpan balik suara sebagai konfirmasi bahwa ketukan telah tercatat saat pandangan mata pedagang tetap tertuju pada pelanggan dan proses peracikan.
3. Penghitungan otomatis total kemasan terjual dan total uang masuk, dilengkapi pengaman koreksi jika terjadi salah ketuk, riwayat waktu transaksi, serta ekspor rekap harian tanpa memerlukan kuota internet.


Karakteristik Pengguna & Lingkungan Kerja:
1. Menggunakan ponsel pintar (smartphone) layar sentuh kelas pemula hingga menengah dengan kapasitas penyimpanan dan spesifikasi perangkat keras yang terbatas.
2. Beroperasi di ruang terbuka (outdoor) di bawah paparan sinar matahari langsung sehingga membutuhkan tampilan antarmuka dengan tingkat kontras warna yang tinggi dan mudah terbaca sekilas.
3. Bekerja dalam kondisi mobilitas tinggi dengan jari yang sering basah oleh es atau air, sehingga membutuhkan tombol berukuran ekstra besar yang responsif terhadap ketukan cepat berturut-turut.



---

## Arsitektur Prompt (Prompt Layering)

Pengembangan aplikasi melalui IBM Bob dirancang menggunakan arsitektur 3-Layer Prompting untuk memastikan AI Agent menghasilkan kode yang menyeluruh, ringan, bebas dependensi jaringan, dan sesuai dengan konteks penggunaan di lapangan:

Layer 1 — Role & Context (Peran & Konteks Sistem)
- Yang Diterapkan: Menetapkan peran AI Agent sebagai senior frontend dan mobile-first web engineer dengan identitas proyek "Kasir Kilat Es Teh". Layer ini memuat konteks masalah nyata pedagang es teh keliling saat menghadapi gelombang pelanggan serta batasan arsitektur mutlak: satu file `index.html` (inline CSS & inline JS), nol pustaka atau framework eksternal, dan beroperasi 100% offline.
- Tujuan Layer: Mengarahkan keputusan arsitektural AI Agent agar memilih pendekatan teknologi browser bawaan (native) yang ringan dan instan dibuka tanpa koneksi internet, sekaligus menyelaraskan desain antarmuka dengan keterbatasan fisik dan waktu pengguna di lapangan.


Layer 2 — Task & Requirements (Tugas & Spesifikasi Fungsional)
- Yang Diterapkan: Menjabarkan tujuh spesifikasi fungsional secara terperinci:
1. Dua tombol aksi utama berdampingan untuk Gelas (Rp 5.000) dan Plastik (Rp 3.500).
2. Tampilan live counter jumlah unit terjual beserta subtotal Rupiah tepat di atas masing-masing tombol.
3. Sintesis suara kencringan uang koin melalui Web Audio API, setiap kali tombol ditekan (disertai kontrol mute/unmute).
4. Panel ringkasan otomatis untuk Total Kemasan Terjual dan Total Uang Masuk dalam format mata uang Rupiah.
5. Pengaman jam sibuk berupa tombol koreksi `-1` per varian, tombol Reset dengan dialog konfirmasi, dan penyimpanan otomatis ke `localStorage`.
6. Panel Log Riwayat Ketukan yang mencatat setiap penambahan (`+1`) maupun koreksi (`-1`) lengkap dengan stempel waktu lokal (`HH:MM:SS`).
7. Dua fitur Ekspor Ringkasan Harian tanpa internet, yakni Salin Laporan (teks ringkasan siap tempel ke WhatsApp) dan Unduh CSV (file laporan lengkap beserta log transaksi).

- Tujuan Layer: Menghilangkan ambiguitas kebutuhan pengguna dan memastikan AI Agent menerjemahkan setiap aturan bisnis—mulai dari struktur harga, posisi elemen visual, umpan balik audio, mitigasi kesalahan input, hingga pelaporan harian—menjadi fitur yang terintegrasi penuh dalam bahasa Indonesia.


Layer 3 — Constraints & Output (Batasan Teknis & Standar Kualitas Keluaran)
- Yang Diterapkan: Mengunci format keluaran menjadi satu file `index.html` utuh dengan standar rekayasa penggunaan CSS custom properties, skema warna kontras untuk keterbacaan di bawah sinar matahari, standar aksesibilitas teks WCAG AA, tata letak responsif mobile-first dengan `touch-action: manipulation` untuk mencegah jeda ketukan (tap delay) maupun zoom tidak sengaja, pemanfaatan native browser Blob & Clipboard API, nol console error, serta struktur komentar kode yang rapi per bagian.
- Tujuan Layer: Berfungsi sebagai pagar pengaman kualitas (quality guardrail) agar kode yang dihasilkan AI Agent stabil dijalankan langsung di browser ponsel pintar, responsif terhadap ketukan jari berkecepatan tinggi, mudah dipelihara, dan siap pakai tanpa tahap kompilasi tambahan.