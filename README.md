# Virtual Learning Environment - Moodle 3.3.2+
<h1 align="center"><img src="https://github.com/DenyRamdhany/moodle3.3x/blob/master/pictures/pic1.png"></h1>

[Sekilas Tentang](#sekilas-tentang) | [Instalasi](#instalasi) | [Konfigurasi](#konfig) | [Cara Pemakaian](#cara) | [Pembahasan](#bahas) | [Referensi](#dapus)
:---:|:---:|:---:|:---:|:---:|:---:

# Sekilas Tentang
[`^ kembali ke atas ^`](#)

**Moodle** (*Modular Object Oriented Dynamic Learning Environment*) merupakan sebuah aplikasi CMS (*content management system*) berbasis web untuk keperluan LMS (*Lecture Management System*). Tujuan dari aplikasi ini adalah menciptakan ruang kelas digital sehingga siswa dapat mengaksesnya dari mana saja bahkan ketika jauh dari sekolahnya. Moodle pertama kali dikembangkan oleh Martin Dougiamas pada tahun 1999 dan langsung mematenkan akronim Moodle serta domain <a href=http://moodle.org>Moodle</a>. Hingga tahun 2017 ini Moodle sudah mencapai versi 3.3x dan sudah digunakan di lebih dari 80.000 universitas dan sekolah di 230 negara termasuk Institut Pertanian Bogor.



# Instalasi
[`^ kembali ke atas ^`](#)

### Kebutuhan hardware minimum:
- 500MB ruang kosong pada disk untuk aplikasi & data
- 1Ghz single core processor
- 512MB RAM

### Kebutuhan software minimum:
- Sistem operasi server
- Web server aktif (Apache, Ngix, IIS atau sejenisnya)
- PHP 5.6.5
- MySql Server 5.5.31

### Proses Instalasi:
#### Prequisite
1. Masuk ke server melalui koneksi SSH (di sini saya menggunakan Linux sebagai host). user ssh yang saya gunakan adalah **user** dan server berada pada IP **192.168.1.19**.
    ```
    $ ssh user@192.168.1.19
    ```
2. Tambahkan repository untuk PHP dan pastikan software list pada server sudah diupdate (gunakan user dengan hak **root**).
    ```
    # add-apt-repository ppa:ondrej/php
    # apt update
    ```
3. Instal paket-paket prasyarat yang dibutuhkan oleh Moodle.
    ```
    # apt install apache2 php phpmyadmin mysql-server php-mysql libapache2-mod-php php-gd php-curl php-xmlrpc php-intl php-soap php-zip 
    ```
4. Buat database yang nantinya digunakan oleh Moodle.
    ```
    # mysql -u root -p
    > <masukan password>
    > CREATE DATABASE moodle;
    > exit
    ```
5. Ubah konfigurasi pada file ``php.ini`` sehingga sesuai dengan kebutuhan, save, lalu restart web server.
    ```
    # nano /etc/php/7.1/apache2/php.ini
    
      post_max_size = 32MB
      upload_max_filesize = 128MB
      
    # service apache2 restart
    ```
    
#### Main Package
1. Masuk ke root directory dari web server. Pada Ubuntu server secara default terletak pada ``/var/www/html/``
    ```
    # cd /var/www/html/
    ```
2. Download dan ekstrak paket Moodle dari situs <a href=https://download.moodle.org/stable33/moodle-latest-33.tgz>Official Release</a> Moodle (ukuran file sekitar 55MB).
    ```
    # wget "https://download.moodle.org/stable33/moodle-latest-33.tgz"
    # tar -zxvf moodle-latest-33.tgz
    ```
3. Buat direktori untuk menyimpan data dari Moodle dengan nama ``moodledata`` pada lokasi satu tingkat diatas root directory web server. Hal ini direkomendasikan agar direktori ini tidak dapat diakses melalui URL.
    ```
    # mkdir /var/www/moodledata
    ```
4. ubah status kepemilikan dan group direktori ``moodle`` yang tadi telah diekstrak dan ``moodledata`` yang sebelumnya dibuat, menjadi milik ``www-data`` sehingga web server memiliki akses untuk mengubah konten dari direktori tersebut.
    ```
    # chown www-data:www-data -R /var/www/html/moodle
    # chown www-data:www-data -R /var/www/moodledata
    ```

#### Web Installation
1. buka alamat dari web server pada aplikasi web browser di komputer client. Dalam kasus ini saya menggunakan alamat ``http://192.168.1.19/moodle`` maka akan tampil halaman awal moodle seperti gambar berikut. Silahkan pilih bahasa untuk aplikasi dan click **Next**
    <img src="https://github.com/DenyRamdhany/moodle3.3x/blob/master/pictures/moodle1.png">
2. 
