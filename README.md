# Laporan-web-server-
# Kelebihan Web Server Apache
Web Server Apache memiliki beberapa keunggulan yang membuatnya banyak digunakan oleh pengelola website, baik skala kecil maupun besar.
# a. Bersifat Open Source dan Gratis
Apache dapat digunakan tanpa biaya lisensi. Pengguna juga memiliki kebebasan untuk memodifikasi kode sumber sesuai kebutuhan. Hal ini membuat Apache menjadi salah satu web server paling populer di dunia.

# b. Mudah Dikonfigurasi
Apache memiliki struktur konfigurasi yang sederhana dan mudah dipahami. File konfigurasi seperti httpd.conf memungkinkan administrator melakukan pengaturan dengan fleksibel.

# c. Mendukung Berbagai Sistem Operasi
Apache dapat dijalankan pada banyak platform, seperti Linux, Windows, macOS, dan berbagai varian Unix. Hal ini meningkatkan kompatibilitas dan kemudahan implementasi.

# d. Memiliki Dokumentasi Lengkap dan Komunitas Besar
Dokumentasi resmi Apache sangat lengkap. Selain itu, komunitas yang besar membuat pengguna mudah menemukan solusi saat terjadi masalah.

# e. Mendukung Banyak Modul Tambahan
Apache menyediakan berbagai modul seperti:
- mod_ssl (untuk HTTPS),
- mod_rewrite (untuk rewriting URL),
- mod_proxy (untuk proxy server),
- dan modul lain yang dapat diaktifkan sesuai kebutuhan.
Modul-modul ini membuat Apache sangat fleksibel.

# f. Stabil dan Telah Teruji
Apache sudah digunakan selama bertahun-tahun di berbagai lingkungan produksi, sehingga stabilitasnya tidak diragukan lagi.

# Kekurangan Web Server Apache
Di balik kelebihannya, Apache juga memiliki beberapa kelemahan yang perlu diperhatikan.
# a. Kurang Efisien untuk Koneksi dalam Jumlah Besar
Arsitektur Apache yang berbasis proses atau thread membuat penggunaan resource meningkat saat menangani ribuan koneksi bersamaan. Web server modern seperti Nginx lebih efisien untuk trafik besar.

# b. Konsumsi Resource Lebih Tinggi
Apache cenderung memakan RAM dan CPU lebih banyak, terutama jika banyak modul aktif. Hal ini dapat menjadi masalah pada server dengan spesifikasi rendah.

# c. Performa Default Tidak Secepat Web Server Modern
Dalam menyajikan static content seperti gambar, CSS, atau JavaScript, Apache umumnya lebih lambat dibandingkan web server lain seperti Nginx atau LiteSpeed.

# d. Pengaturan Lebih Kompleks untuk Performa Tinggi
Meskipun mudah dikonfigurasi untuk penggunaan dasar, konfigurasi Apache untuk kebutuhan high performance membutuhkan keahlian teknis yang lebih tinggi.

# e. Beberapa Modul Sudah Tidak Dikembangkan Secara Aktif
Karena Apache merupakan proyek lama, tidak semua modul mendapatkan pembaruan rutin sesuai perkembangan teknologi web modern.
