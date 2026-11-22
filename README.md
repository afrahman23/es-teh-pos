# es-teh-pos

3 Layer Prompt
### LAYER 1 — ROLE & CONTEXT
Bertindaklah sebagai senior frontend dan mobile-first web engineer menggunakan IBM Bob.
Nama proyek: "Kasir Kilat Es Teh Keliling", sebuah aplikasi web Point-of-Sale (POS) penghitung ketukan (tap-counter) untuk membantu pedagang keliling es-teh. Pedagang es-teh umumnya melayani gelombang pelanggan dalam jumlah banyak sekaligus sehingga tidak sempat mencatat dan menghitung secara manual berapa banyak kemasan gelas dan plastik yang telah terjual.
Batasan utama: satu file HTML tunggal (single HTML file), hanya menggunakan inline CSS dan inline JS, tanpa pustaka (library) eksternal, tanpa framework, dan wajib berjalan 100% offline.

### LAYER 2 — TASK & REQUIREMENTS
Bangun aplikasi tap-counter tanpa jeda (zero-latency) untuk melacak penjualan, riwayat transaksi, dan pendapatan harian pada dua varian kemasan es-teh:
- Gelas = Rp 5.000
- Plastik = Rp 3.500

Requirements:
(1) Dua Tombol Aksi Utama: Dua tombol sentuh berukuran besar yang diletakkan berdampingan dengan label "GELAS" (Rp 5.000) dan "PLASTIK" (Rp 3.500) untuk ditekan pedagang setiap kali satu unit terjual saat melayani gelombang pembeli.
(2) Penghitung Langsung (Live Counter) di Atas Setiap Tombol: Tepat di atas tombol "GELAS" dan tepat di atas tombol "PLASTIK", tampilkan angka penghitung langsung berukuran besar dan jelas yang menunjukkan jumlah unit terjual untuk masing-masing kemasan tersebut (beserta subtotalnya dalam Rupiah).
(3) Efek Suara Kencringan Koin: Setiap ketukan pada salah satu tombol memicu efek suara kencringan uang koin logam yang jernih secara sintetis melalui Web Audio API (tanpa file audio eksternal, dilengkapi tombol mute/unmute).
(4) Ringkasan Total Penjualan & Uang Masuk: Tampilkan panel ringkasan utama yang memuat gabungan total kemasan terjual (Total Kemasan Terjual) dan total uang yang masuk (Total Uang Masuk, diformat dalam Rupiah Indonesia, misalnya Rp 42.500).
(5) Pengaman Jam Sibuk & Penyimpanan Otomatis: Sertakan tombol koreksi "-1" berukuran kecil pada masing-masing varian untuk mengantisipasi ketukan ganda yang tidak disengaja, tombol "Reset" dengan dialog konfirmasi untuk memulai shift baru, serta penyimpanan otomatis di localStorage agar data penjualan dan riwayat tidak hilang apabila halaman tidak sengaja dimuat ulang (refresh).
(6) Log Riwayat Ketukan: Catat secara otomatis setiap ketukan (+1 Gelas, +1 Plastik, maupun koreksi -1) lengkap dengan stempel waktu lokal (HH:MM:SS, misalnya "14:05:22 — +1 Gelas (+Rp 5.000)") secara berurutan dari yang terbaru (reverse-chronological) di dalam panel riwayat ringkas yang dapat digulir (scrollable) di bagian bawah kontrol utama, dan simpan di localStorage.
(7) Ekspor Ringkasan Harian: Sediakan dua tombol ekspor 100% offline di bagian bawah antarmuka:
- "Salin Laporan": Menyalin teks ringkasan harian yang rapi dan terformat (tanggal, jumlah & subtotal Gelas, jumlah & subtotal Plastik, total kemasan terjual, serta total uang masuk) ke clipboard agar siap langsung ditempel ke WhatsApp atau catatan, disertai notifikasi toast singkat.
- "Unduh CSV": Membuat dan mengunduh file .csv lokal (dengan nama `laporan-esteh-YYYY-MM-DD.csv`) yang berisi rincian ringkasan harian diikuti seluruh log riwayat ketukan berstempel waktu.
Seluruh teks antarmuka (UI), label, stempel waktu, pesan notifikasi toast, dan format mata uang wajib menggunakan Bahasa Indonesia.

### LAYER 3 — CONSTRAINTS & OUTPUT
Hasilkan satu file index.html lengkap. Gunakan CSS custom properties untuk tema tampilan, gaya kontras tinggi yang mudah dibaca di ruang terbuka di bawah sinar matahari terang (outdoor-readable), rasio kontras teks memenuhi standar WCAG AA, tata letak responsif mobile-first dengan tombol ekstra besar yang ramah ibu jari (menggunakan touch-action: manipulation untuk menghilangkan jeda ketukan pada perangkat seluler), gunakan native browser Blob API dan Clipboard API untuk ekspor offline, bebas dari console error, serta berikan komentar kode yang jelas di setiap bagian.