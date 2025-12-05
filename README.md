# 📄 LAPORAN WEB SERVER APACHE
### 👥 Informasi Kelompok dan Spesifikasi Lingkungan Praktik
| Peran | Nama Lengkap | Kelas |
| :--- | :--- | :--- |
| **Ketua Kelompok** | Andrea Fredericka G.S | XI TJKT 1 |
| Anggota 1 | Soraya Oktaviani Sopian | XI TJKT 1 |
| Anggota 2 | Elis Lisnawati | XI TJKT 1 |
| Anggota 3 | Risa Solaiha M | XI TJKT 1 |
| Anggota 4 | Sri Ayu A | XI TJKT 1 |
| **Nama Sekolah/Institusi** | SMK NEGERI 1 SOREANG | |

# 🔥 Pengertian Apache
Apache adalah web server open-source yang digunakan untuk menerima permintaan dari browser dan menampilkan halaman web ke pengguna. Apache populer karena stabil, aman, fleksibel, serta mendukung banyak modul dan berbagai sistem operasi.

# 🛠️ 1. TAHAPAN-TAHAPAN MENGINSTAL WEB SERVER APACHE
# Menyiapkan Debian Server 🐧
Siapkan server Debian yang sudah punya IP Address dan bisa diakses dari jaringan LAN.
Atur Repository agar bisa digunakan untuk instalasi software.
Coba akses server lewat SSH pakai CMD dan WinSCP untuk memastikan koneksinya sudah berfungsi.

# ▪️ Instalasi Apache Web Server 🌐
1.Login dan Update Paket
```bash
apt update & apt upgrade
```
2.Instal Apache
```bash
apt install apache2
```
3.Aktifkan Apache dan pastikan berjalan
```bash
systemctl enable apache2
systemctl start apache2
systemctl status apache2
```
4.Uji dari browser: http://ip-server

# ▪️ Instalasi PHP 🐘
1.Instal PHP Dasar
```bash
apt install php
```
3.Instalasi Extension PHP Tambahan:
```bash
apt install php-common php-xml php-curl php-zip php-gd php-mbstring php-intl php-json php-soap php-mysql
```

# ▪️ Pastikan PHP Sudah Berjalan 🚀
1.Buat file uji:
```bash
nano /var/www/html/info.php
```
2.tambahkan script berikut:
```bash
<?php phpinfo(); ?>
```
3.Akses dari browser: http://ip-server/info.php

# ▪️ Menambahkan SSL Self-Signed Certificate 🔐
1.Instal OpenSSL dan aktifkan modul SSL
```bash
apt install openssl
a2enmod ssl
```
2.Buat folder untuk sertifikat
```bash
mkdir /etc/apache2/ssl
```
3.Buat sertifikat self-signed
```bash
openssl req -x509 -nodes -days 365 -newkey
```
4.contoh pengisian: 
• Country Name (2 letter code) [AU]: ID
• State or Province Name (full name) [Some-    State]: Jawa Barat
• Organization Name (eg, company) [Internet   Widgits Pty Ltd]: SMKN 1 Soreang
• Common Name (e.g. server FQDN or YOUR       name) []: server.local

# ▪️ Konfigurasi Virtual Host HTTPS ⚙️📄
1.Salin file konfigurasi default
```bash
cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/000-default-ssl.conf
```
2.Edit supaya bisa memasukan konfigurasi file SSL
```bash
nano /etc/apache2/sites-available/000-default-ssl.conf
```
3.Isi dengan konfigurasi berikut:
```bash
VirtualHost *:443>
  ServerAdmin admin@localhost
  DocumentRoot /var/www/html
  ServerName server.local

  SSLEngine on
  SSLCertificateFile/etc/apache2/ssl
  /selfsigned.crt
  SSLCertificateKeyFile/etc                   /apache2/ssl/selfsigned.key

  <Directory /var/www/html>
   AllowOverride All
   Options Indexes FollowSymLinks
   Require all granted
  </Directory>

   ErrorLog ${APACHE_LOG_DIR}/error.log
   CustomLog ${APACHE_LOG_DIR}/access.log      combined
   </VirtualHost>
```
   Simpan (Ctrl + O, Enter), lalu keluar       (Ctrl + X).

# ▪️ Aktifkan HTTPS dan Modul Rewrite ⚙️
1.Aktifkan situs SSL dan modul rewrite
```bash
a2ensite 000-default-ssl.conf
a2enmod rewrite
systemctl reload apache2
```bash
2.Uji dari browser: https://ip-server

# ▪️ Redirect HTTP ke HTTPS (Opsional) 🔗
1.Untuk melakukan redirect (mengalihkan), baiknya server harus menggunakan IP statis, dan DNS server bekerja dengan baik, jika tidak sebaiknya skip dulu tahapan di bawah!
2.Edit file konfigurasi HTTP:
```bash
nano /etc/apache2/sites-available/000-default.conf
```
3.Tambahkan perintah redirect di dalam <VirtualHost *:80>:
```bash
<VirtualHost *:80>
  ServerAdmin admin@localhost
  ServerName server.local
  DocumentRoot /var/www/html

  # ▪️ Redirect semua akses HTTP ke HTTPS
  Redirect "/" "https://server.local/"

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log      combined
</VirtualHost>
```
4.Kita bisa menyesuaikan nama domain dan target redirect 
5.Reload Apache:
```bash
systemctl reload apache2
```

# ▪️ Uji Coba Web Apache
1.Pastikan Apache Berjalan
Sebelum uji coba:
```bash
systemctl status apache2
```
Jika muncul active (running) → siap diuji.

2.Uji Coba dari Browser 
 A. Gunakan IP server
* Buka browser (Chrome/Firefox)
* Ketik di address bar:
Contoh:
http://192.168.1.10

B. Jika Apache Berhasil
Akan muncul salah satu tampilan:
Halaman default “Apache2 Ubuntu Default Page”

Atau halaman yang buat di index.html

Jika muncul, berarti Apache sukses berjalan.

3.Uji Coba dari Server Menggunakan CURL

Jika Apache berjalan, akan muncul isi HTML seperti:
<html><body><h1>It works!</h1></body></html>

 4. Uji Coba Folder Dokumen Web
Coba buat file sederhana:
```bash
nano /var/www/html/test.html
```
Isi:
<h2>Apache Test OK</h2>
Simpan, lalu akses:
http://IP-Server/test.html

Jika terbuka → konfigurasi Apache dan folder web tidak ada masalah.

# ⭐ 2. KELEBIHAN DAN KEKURANGAN WEB SERVER APACHE
Web Server Apache memiliki beberapa keunggulan yang membuatnya banyak digunakan oleh pengelola website, baik skala kecil maupun besar.
# Kelebihan Web Server Apache
## ▪️ Bersifat Open Source dan Gratis
Apache dapat digunakan tanpa biaya lisensi. Pengguna juga memiliki kebebasan untuk memodifikasi kode sumber sesuai kebutuhan. Hal ini membuat Apache menjadi salah satu web server paling populer di dunia.

## ▪️ Mudah Dikonfigurasi
Apache memiliki struktur konfigurasi yang sederhana dan mudah dipahami. File konfigurasi seperti httpd.conf memungkinkan administrator melakukan pengaturan dengan fleksibel.

## ▪️ Mendukung Berbagai Sistem Operasi
Apache dapat dijalankan pada banyak platform, seperti Linux, Windows, macOS, dan berbagai varian Unix. Hal ini meningkatkan kompatibilitas dan kemudahan implementasi.

## ▪️ Memiliki Dokumentasi Lengkap dan Komunitas Besar
Dokumentasi resmi Apache sangat lengkap. Selain itu, komunitas yang besar membuat pengguna mudah menemukan solusi saat terjadi masalah.

## ▪️ Mendukung Banyak Modul Tambahan
Apache menyediakan berbagai modul seperti:
- mod_ssl (untuk HTTPS),
- mod_rewrite (untuk rewriting URL),
- mod_proxy (untuk proxy server),
- dan modul lain yang dapat diaktifkan sesuai kebutuhan.
Modul-modul ini membuat Apache sangat fleksibel.

## ▪️ Stabil dan Telah Teruji
Apache sudah digunakan selama bertahun-tahun di berbagai lingkungan produksi, sehingga stabilitasnya tidak diragukan lagi.

# Kekurangan Web Server Apache
Di balik kelebihannya, Apache juga memiliki beberapa kelemahan yang perlu diperhatikan.
## ▪️ Kurang Efisien untuk Koneksi dalam Jumlah Besar
Arsitektur Apache yang berbasis proses atau thread membuat penggunaan resource meningkat saat menangani ribuan koneksi bersamaan. Web server modern seperti Nginx lebih efisien untuk trafik besar.

## ▪️ Konsumsi Resource Lebih Tinggi
Apache cenderung memakan RAM dan CPU lebih banyak, terutama jika banyak modul aktif. Hal ini dapat menjadi masalah pada server dengan spesifikasi rendah.

## ▪️ Performa Default Tidak Secepat Web Server Modern
Dalam menyajikan static content seperti gambar, CSS, atau JavaScript, Apache umumnya lebih lambat dibandingkan web server lain seperti Nginx atau LiteSpeed.

## ▪️ Pengaturan Lebih Kompleks untuk Performa Tinggi
Meskipun mudah dikonfigurasi untuk penggunaan dasar, konfigurasi Apache untuk kebutuhan high performance membutuhkan keahlian teknis yang lebih tinggi.

## ▪️ Beberapa Modul Sudah Tidak Dikembangkan Secara Aktif
Karena Apache merupakan proyek lama, tidak semua modul mendapatkan pembaruan rutin sesuai perkembangan teknologi web modern.

# 📂 3. Struktur Penggunaan Kode HTML Website

Untuk kode HTML, pada bagian **tampilan depan (frontend)** kami menggunakan kode yang sama.  
Sedangkan untuk bagian **data pribadi atau identitas diri**, kami menggunakan kode yang berbeda untuk masing-masing individu.

Kami secara jujur memanfaatkan **AI** agar proses pembuatan menjadi lebih cepat, efisien, dan menghasilkan tampilan yang lebih baik.

## Proses Pemindahan File ke Server

Langkah-langkah yang kami lakukan adalah sebagai berikut:

1. Mencari file HTML di server.
2. Masuk ke direktori file server.
3. Mencari folder: www
4. Di dalam folder tersebut terdapat file HTML.
5. Kami mengunggah seluruh file yang dibutuhkan untuk website kami ke dalam folder tersebut.

Dengan cara ini, seluruh komponen website dapat berjalan dan ditampilkan dengan baik di server.

# 🧩 4. Kendala dan Solusi
Kendala Yang Dialami Beserta Solusinya.

## ▪️ Tidak Dapat Melakukan Login ke WinSCP dan SSH Root

Kendala:
Pengguna tidak dapat melakukan login ke WinSCP dan SSH root karena akses ke server dibatasi oleh jaringan internal. Hal ini membuat proses autentikasi gagal ketika mencoba masuk dari jaringan luar.

Solusi:
Menggunakan VPN untuk terhubung ke jaringan internal terlebih dahulu sehingga akses login ke WinSCP dan SSH root dapat berjalan dengan normal.

## ▪️ Ketidakstabilan Akses Jaringan

Kendala:
Koneksi jaringan yang tidak konsisten menghambat proses pemindahan data dan aktivitas administrasi server.

Solusi:
Menggunakan jaringan yang lebih stabil (misalnya koneksi LAN) serta melakukan pengecekan perangkat jaringan seperti router atau access point untuk mengurangi gangguan.

## ▪️ Server Belum Diaktifkan

Kendala:
Server milik guru belum diaktifkan pada saat proses pengerjaan, sehingga seluruh aktivitas terkait akses server tidak dapat dilakukan.

Solusi:
Melakukan konfirmasi terlebih dahulu kepada guru atau penanggung jawab server mengenai jadwal penyalaan server sebelum memulai pekerjaan.

## ▪️ Kesulitan Awal dalam Menambahkan Gambar pada Website

Kendala:
Pada tahap awal, menambahkan gambar ke dalam website terasa sulit karena belum memahami struktur direktori dan path file.

Solusi:
Mempelajari struktur folder proyek serta cara penempatan file gambar. Setelah memahami alurnya, proses penambahan gambar menjadi lebih mudah.

## ▪️ Emoji Tidak Tampil dengan Benar

Kendala:
Emoji tidak muncul sebagaimana mestinya dan berubah menjadi tanda tanya (“?”) saat program dijalankan. Hal ini diduga terkait pengaturan encoding atau font yang tidak mendukung.

Solusi:
Mengubah encoding file maupun server menjadi UTF-8 serta menggunakan font yang mendukung karakter emoji. Jika perlu, emoji dapat diganti dengan icon berbasis gambar atau SVG.

# ▪️ Dokumentasi Video Pengerjaan
Seluruh proses pengerjaan dan penjelasan materi telah direkam dan diunggah ke YouTube.

**Link Video YouTube:**
[![Thumbnail Video YouTube](https://img.youtube.com/vi/z4dJuHGqQ8o/maxresdefault.jpg)](https://youtu.be/z4dJuHGqQ8o)
