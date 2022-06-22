# LAB11

|  | |
| ----------- | ----------- |
| <b> Nama     | Aditya Bani Isro       |
| <b> NIM     | 312010134       |
| <b> Kelas   | TI.20.A.1        |
| <b> Matakuliah   | Pemrograman Web        |
| <b> Praktikum     | <a href="#p11">11</a>, <a href="#p12">12</a> & <a href="#p13">13</a></td>  |

<div id="p11">

# <spaan style="color: blue">Praktikum 11 | PHP Framework (Codeigniter)</span>

## Langkah langkah praktikum
## Persiapan
Sebelum memulai menggunakan Framework Codeigniter, perlu dilakukan konfigurasi
pada webserver. Beberapa ekstensi PHP perlu diaktifkan untuk kebutuhan
pengembangan Codeigniter 4.
Berikut beberapa ekstensi yang perlu diaktifkan:
- php-json ekstension untuk bekerja dengan JSON;
- php-mysqlnd native driver untuk MySQL;
- php-xml ekstension untuk bekerja dengan XML;
- php-intl ekstensi untuk membuat aplikasi multibahasa;
- libcurl (opsional), jika ingin pakai Curl.

Untuk mengaktifkan ekstentsi tersebut, melalu XAMPP Control Panel, pada bagian
Apache klik ``Config -> PHP.ini``

![img1](assets/img/1.png)

Pada bagian extention, hilangkan tanda ; (titik koma) pada ekstensi yang akan
diaktifkan. Kemudian simpan kembali filenya dan restart Apache web server.

![img2](assets/img/2.PNG)

## Instalasi  Codeigniter 4
Untuk melakukan instalasi Codeigniter 4 dapat dilakukan dengan dua cara, yaitu cara manual dan menggunakan composer. Pada praktikum ini kita menggunakan cara
manual.
- Unduh Codeigniter dari website https://codeigniter.com/download
- Extrak file zip Codeigniter ke direktori htdocs/lab11_ci.
- Ubah nama direktory framework-4.x.xx menjadi ci4.
- Buka browser dengan alamat http://localhost/lab11_ci/ci4/public/

![img3](assets/img/3.PNG)

## Menjalankan CLI (Command Line Interface)
Codeigniter 4 menyediakan CLI untuk mempermudah proses development. Untuk
mengakses CLI buka terminal/command prompt.

![img4](assets/img/2.1.PNG)

Arahkan lokasi direktori sesuai dengan direktori kerja project dibuat ``(xampp/htdocs/lab11_ci/ci4/)``.

Perintah yang dapat dijalankan untuk memanggil CLI Codeigniter adalah :
```
php spark
```

![img5](assets/img/2.2.PNG)

## Mengaktifkan Mode Debugging
- Ketik ``php spark serve`` pada CLI untuk menjalankan.

![img6](assets/img/00.PNG)

- Menampilkan pesan error, untuk mencobanya ubah kode file ``app/Controllers/home.php``, hapus ;nya.

![img7](assets/img/3.1.PNG)

- Ketik ``http://localhost:8080`` pada browser. Berikut tampilan error nya.

![img8](assets/img/3.2.PNG)

- Kemudian, ubah nama file ``env`` menjadi ``.env``. Masuk ke dalam filenya, hapus tanda ``#`` pada ``CI_ENVIRONMENT =``

![img9](assets/img/3.3.PNG)

- Refresh url sebelumnya, Berikut tampilan error nya.

![img10](assets/img/3.4.PNG)

## Struktur Direktori

![img11](assets/img/3.5.PNG)

## Routing and Controller
Router terletak pada file ``app/config/Routes.php``

## Membuat Route Baru
Tambahkan kode berikut di dalam ``Routes.php``
```php
$routes->get('/about', 'Page::about');
$routes->get('/contact', 'Page::contact');
$routes->get('/faqs', 'Page::faqs');
```

![img8](assets/img/3.6.PNG)

Untuk mengetahui route yang ditambahkan sudah benar, buka CLI dan jalankan
perintah berikut.
```
php spark routes
```
![img8](assets/img/3.7.PNG)

Selanjutnya coba akses route yang telah dibuat dengan mengakses alamat url http://localhost:8080/about

![img8](assets/img/3.8.PNG)

## Membuat Controller
Selanjutnya adalah membuat Controller Page. Buat file baru dengan nama ``page.php`` pada direktori Controller kemudian isi kodenya seperti berikut.
```php
<?php
namespace App\Controllers;
class Page extends BaseController
{
    public function about()
    {
        echo "Ini halaman About";
    }

    public function contact()
    {
        echo "Ini halaman Contact";
    }

    public function faqs()
    {
        echo "Ini halaman FAQ";
    }
}
```
![img8](assets/img/4.1.PNG)

Selanjutnya refresh Kembali browser, maka akan ditampilkan hasilnya yaitu halaman sudah dapat diakses.

![img8](assets/img/4.2.PNG)

- Auto Routing
Secara default fitur autoroute pada Codeiginiter sudah aktif. Untuk mengubah status autoroute dapat mengubah nilai variabelnya. Untuk menonaktifkan ubah nilai ``true`` menjadi ``false``.
```php
$routes->setAutoRoute(true);
```
![img8](assets/img/4.3.PNG)

Tambahkan method baru pada Controller Page seperti berikut.
```php
public function tos()
{
    echo "ini halaman Term of Services";
}
```
![img8](assets/img/4.4.PNG)

Method ini belum ada pada routing, sehingga cara mengaksesnya dengan menggunakan alamat: http://localhost:8080/page/tos

![img8](assets/img/4.5.PNG)

## Membuat View
Selanjutnya adalam membuat view untuk tampilan web agar lebih menarik. Buat file baru dengan nama ``about.php`` pada direktori view ``(app/view/about.php)`` kemudian isi kodenya seperti berikut.
```php
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <title><?= $title; ?></title>
    </head>
    <body>
        <h1><?= $title; ?></h1>
        <hr>
        <p><?= $content; ?></p>
    </body>
</html>
```
![img8](assets/img/5.1.PNG)

Ubah ``method about`` pada class ``Controller Page`` menjadi seperti berikut:
```php
public function about()
{
    return view('about', [
        'title' => 'Halaman About',
        'content' => 'Ini adalah halaman abaut yang menjelaskan tentang isi halaman ini.'
        ]);
}
```
![img8](assets/img/5.2.PNG)

Kemudian lakukan refresh pada halaman tersebut.
![img8](assets/img/5.3.PNG)

## Membuat Layout Web dengan CSS
Buat file css pada direktori ``public`` dengan nama ``style.css`` (copy file dari praktikum ``lab4_layout``. Kita akan gunakan layout yang pernah dibuat pada praktikum 4.

![img8](assets/img/6.1.PNG)

Kemudian buat folder template pada direktori view kemudian buat file ``header.php`` dan ``footer.php``
```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title><?= $title; ?></title>
    <link rel="stylesheet" href="<?= base_url('/style.css');?>">
</head>
<body>
    <div id="container">
        <header>
            <h1>Layout Sederhana</h1>
        </header>
        <nav>
            <a href="<?= base_url('/');?>" class="active">Home</a>
            <a href="<?= base_url('/artikel');?>">Artikel</a>
            <a href="<?= base_url('/about');?>">About</a>
            <a href="<?= base_url('/contact');?>">Kontak</a>
        </nav>
        <section id="wrapper">
            <section id="main">
```
![img8](assets/img/6.2.PNG)

File ``app/view/template/footer.php``
![img8](assets/img/6.3.PNG)

Kemudian ubah file ``app/view/about.php`` seperti berikut.
```php
<?= $this->include('template/header'); ?>
<h1><?= $title; ?></h1>
<hr>
<p><?= $content; ?></p>
<?= $this->include('template/footer'); ?>
```
![img8](assets/img/6.4.PNG)

Selanjutnya refresh tampilan pada alamat http://localhost:8080/about

![img8](assets/img/6.5.PNG)

# Pertanyaan dan Tugas
Lengkapi kode program untuk menu lainnya yang ada pada Controller Page, sehingga semua link pada navigasi header dapat menampilkan tampilan dengan layout yang sama.

# Jawaban
- Ubah isi pada Routes.php menjadi berikut,

![img8](assets/img/7.1.PNG)

- Pada ``Controllers/page.php``, menjadi berikut
```php
<?php
namespace App\Controllers;

class Page extends BaseController
{
    public function rumah()
    {
        return view('rumah', [
        'title' => 'Halaman Home',
        'content' => 'Ini adalah halaman home yang menjelaskan tentang isi
        halaman ini.'
        ]);
    }

    public function about()
    {
        return view('about', [
        'title' => 'Halaman About',
        'content' => 'Ini adalah halaman about yang menjelaskan tentang isi 
        halaman ini.'
        ]);
    }

    public function contact()
    {
        return view('contact', [
        'title' => 'Halaman Contact',
        'content' => 'Ini adalah halaman contact yang menjelaskan tentang isi 
        halaman ini.'
        ]);
    }

    public function artikel()
    {
        return view('artikel', [
        'title' => 'Halaman Artikel',
        'content' => 'Ini adalah halaman artikel yang menjelaskan tentang isi 
        halaman ini.'
        ]);
    }

    public function faqs()
    {
        return view('faqs', [
            'title' => 'Halaman FAQ',
            'content' => 'Ini adalah halaman FAQ yang menjelaskan tentang isi 
            halaman ini.'
            ]);
    }

    public function tos()
    {
        return view('tos', [
        'title' => 'Halaman TOS',
        'content' => 'Ini adalah halaman Terms of Service yang menjelaskan tentang isi 
        halaman ini.'
        ]);
    }
}
```

Pada masing-masing file di dalam Views, buat file baru denga nama : ``rumah.php``,``about.php``,``artikel.php``,``contact.php``,``faqs.php``, dan ``tos.php``. Masukan kode dibawah ini ke semua file tersebut
```php
    <?= $this->include('template/header'); ?>
    <h1><?= $title; ?></h1>
    <hr>
    <p><?= $content; ?></p>
    <?= $this->include('template/footer'); ?>
```
Untuk melihat hasilnya dengan menggunakan
alamat: http://localhost:8080/rumah

![img8](assets/img/finish.PNG)

<div id="p12">

# <span style="color: blue">Praktikum 12 | Framework Lanjutan (CRUD)</span>

## 1. Database
- Jalankan ``Apache, MySql`` pada Xampp, Buat database dengan nama ``lab_ci4`` di http://localhost/phpmyadmin.
- Buat tabel dengan nama ``artikel``.
    ```sql
    CREATE TABLE artikel (
        id INT(11) auto_increment,
        judul VARCHAR(200) NOT NULL,
        isi TEXT,
        gambar VARCHAR(200),
        status TINYINT(1) DEFAULT 0,
        slug VARCHAR(200),
        PRIMARY KEY(id)
    );
    ```
![img27](assets/img/12.1.PNG)
<br>

## 2. Konfigurasi Koneksi Database
- Terletak di folder ``ci4``, file `.env`, Hapus tanda `#`.
![img27](assets/img/12.2.PNG)
<br>

## 3. Membuat Model 
- Terletak di folder `app/Models`, buat file `ArtikelModel.php`.
![img27](assets/img/12.3.PNG)
<br>

## 4. Membuat Controller 
- Terletak di folder `app/Controllers`, buat file `Artikel.php`.
![img27](assets/img/12.4.PNG)
<br>

## 5. Membuat View pada artikel 
- Terletak di folder `app/Views/artikel`, buat file `index.php`.
![img27](assets/img/12.5.PNG)
<br>

- Buka browser, ketik http://localhost:8080/artikel 
![img32](assets/img/12.6.PNG)
<br>

- Masukkan data ke tabel artikel,
    ```sql
    INSERT INTO artikel (judul, isi, slug) VALUE
    ('Artikel pertama', 'Lorem Ipsum adalah contoh teks atau dummy dalam industri 
    percetakan dan penataan huruf atau typesetting. Lorem Ipsum telah menjadi 
    standar contoh teks sejak tahun 1500an, saat seorang tukang cetak yang tidak 
    dikenal mengambil sebuah kumpulan teks dan mengacaknya untuk menjadi sebuah 
    buku contoh huruf.', 'artikel-pertama'), 
    ('Artikel kedua', 'Tidak seperti anggapan banyak orang, Lorem Ipsum bukanlah 
    teks-teks yang diacak. Ia berakar dari sebuah naskah sastra latin klasik dari 
    era 45 sebelum masehi, hingga bisa dipastikan usianya telah mencapai lebih 
    dari 2000 tahun.', 'artikel-kedua');
    ``` 
![img33](assets/img/12.7.PNG)
<br>

- Refresh kembali browser.
![img34](assets/img/12.8.PNG)
<br>

## 6. Membuat Tampilan detail Artikel
- Terletak di folder `app/Controllers`, edit file `Artikel.php`. Tambah method ``view()``.
![img35](assets/img/12.9.PNG)
<br>

## 7. Membuat View pada Detail
- Terletak di folder `app/Views/artikel`, buat file `detail.php`.
![img36](assets/img/12.10.PNG)
<br>

## 8. Membuat Routing untuk artikel detail
- Terletak di folder `app/Config`, edit file `Routes.php`.
![img36-2](assets/img/12.11.PNG)
<br>

- Klik `Artikel Kedua` pada http://localhost:8080/artikel, untuk pindah ke detailnya.
![img37](assets/img/12.12.PNG)
<br>

## 9. Membuat Menu admin
- Terletak di folder `app/Controller`, edit file `Artikel.php`. Tambah method `admin_index()`.
![img38](assets/img/12.13.PNG)
<br>

- Selanjutnya, akses kembali folder `app/Views/artikel`, buat file `admin_index.php`.
    ```php
    <?= $this->include('template/admin_header'); ?>
    <table class="table table-bordered table-hover">
        <thead>
            <tr class="table-primary">
                <th scope="col">ID</th>
                <th scope="col">Judul</th>
                <th scope="col">Status</th>
                <th scope="col">Aksi</th>
            </tr>
        </thead>
        <tbody>
            <?php if($artikel): foreach($artikel as $row): ?>
            <tr>
                <td><?= $row['id']; ?></td>
                <td>
                    <b><?= $row['judul']; ?></b>
                    <p><small><?= substr($row['isi'], 0, 50); ?></small></p>
                </td>
                <td><?= $row['status']; ?></td>
                <td>
                    <a class="btn btn-primary p-1" href="<?= base_url('/admin/artikel/edit/' . 
                    $row['id']);?>">Ubah</a>
                    <a class="btn btn-danger p-1" onclick="return confirm('Yakin menghapus data?');" href="<?= base_url('/admin/artikel/delete/' . 
                    $row['id']);?>">Hapus</a>
                </td>
            </tr>
            <?php endforeach; else: ?>
            <tr>
                <td colspan="4">Belum ada data.</td>
            </tr>
            <?php endif; ?>
        </tbody>
        <tfoot>
            <tr class="table-primary">
                <th scope="col">ID</th>
                <th scope="col">Judul</th>
                <th scope="col">Status</th>
                <th scope="col">Aksi</th>
            </tr>
        </tfoot>
    </table>
    <?= $this->include('template/admin_footer'); ?>
    ```
<br>

- Buka folder yang ada di ``app/Views/artikel/template``, kemudian buat:
- ``admin_header.php``,
![img38-1](assets/img/12.15.PNG)
<br>

- ``admin_footer.php``
![img38-2](assets/img/12.16.PNG)
<br>

## 10. Membuat Routing untuk menu admin
- Terletak di folder `app/Config`, edit file `Routes.php`.
![img39](assets/img/12.17.PNG)
<br>

- Akses browser dengan http://localhost:8080/admin/artikel.
![img40](assets/img/12.18.PNG)
<br>

## 11. Menambah data untuk Artikel
- Terletak di folder `app/Controller`, edit file `Artikel.php`. Tambah method `add()`.
![img41](assets/img/12.19.PNG)
<br>

- Akses kembali folder `app/Views/artikel`, buat file `form_add.php`.
![img42](assets/img/12.20.PNG)
<br>

- Akses browser dengan http://localhost:8080/admin/artikel/add.
![img43](assets/img/12.21.PNG)
<br>

## 12. Mengubah data pada Artikel
- Terletak di folder `app/Controller`, edit file `Artikel.php`. Tambah method `edit()`.
![img44](assets/img/12.22.PNG)
<br>

- Akses kembali folder `app/Views/artikel`, buat file `form_edit.php`.
![img45](assets/img/12.23.PNG)
<br>

- Akses browser dengan http://localhost:8080/admin/artikel/edit/1 untuk Mengubah artikel pertama.
![img46](assets/img/12.24.PNG)
<br>

## 13. Menghapus data pada Artikel
- Terletak di folder `app/Controller`, edit file `Artikel.php`. Tambah method `delete()`.
![img47](assets/img/12.25.PNG)
<br>

- Akses browser dengan http://localhost:8080/admin/artikel/add untuk membuat artikel ketiga, lalu `kirim`.
![img48](assets/img/12.26.PNG)
<br>

- Untuk mengeceknya ketik di url, http://localhost:8080/artikel kemudian enter.
![img49](assets/img/12.27.PNG)
<br>

- Pergi ke menu admin untuk menghapusnya, http://localhost:8080/admin/artikel, kemudian pilih `hapus`.
![img50](assets/img/12.28.PNG)
<br>

- Artikel berhasil dihapus.
![img51](assets/img/12.29.PNG)

<div id="p13">

# <span style="color: blue">Praktikum 13 | Framework Lanjutan (Modul Login)</span>

## 1. Membuat Table User
- Jalankan ``Apache, MySql`` pada Xampp, Akses browser http://localhost/phpmyadmin.
- Buat tabel dengan nama ``artikel``.
    ```sql
        CREATE TABLE user (
        id INT(11) auto_increment,
        username VARCHAR(200) NOT NULL,
        useremail VARCHAR(200),
        userpassword VARCHAR(200),
        PRIMARY KEY(id)
        );
    ```
![img52](assets/img/13.1.PNG)
<br>

## 2. Membuat Model User
- Terletak di folder `app/Models`, buat file `UserModel.php`.
![img53](assets/img/13.2.PNG)
<br>

## 3. Membuat Controller User
- Terletak di folder `app/Controllers`, buat file `User.php`.
![img54](assets/img/13.3.PNG)

## 4. Membuat View Login
- Terletak di folder `app/Views`, buat folder baru dengan nama `user`, buat file `login.php` di dalamnya.
![img55](assets/img/13.4.PNG)
<br>

## 5. Membuat Database Seeder
- Untuk keperluan uji coba.
- Masuk ke direktori ci4, kemudian ketikkan kode:
``php spark make:seeder UserSeeder``
![img56](assets/img/13.5.PNG)
<br>

- Terletak di folder `app/Database/Seeds`, buka file `UserSeeder.php`, kemudian edit menjadi berikut:
![img57](assets/img/13.6.PNG)
<br>

- Buka kembali CLI, kemudian ketik perintah berikut:
``php spark db:seed UserSeeder``
![img58](assets/img/13.7.PNG)
<br>

- Berikut data yang sudah ditambah pada tabel `user`. Dengan mengakses ``http://localhost/phpmyadmin``.
![img59](assets/img/13.8.PNG)
<br>

- Buka file `.env`, kemudian hapus `#` pada `app.sessionX`
![img61](assets/img/13.9.PNG)
<br>

- Akses kembali url ``http://localhost:8080/user/login``
![img62](assets/img/13.10.PNG)
<br>

## 6. Menambah Auth Filter
- Terletak di folder `app/Filters`, buat file `Auth.php`
![img63](assets/img/13.11.PNG)
<br>

- Kemudian pada folder `app/Config`, edit isi file `Filters.php` menjadi berikut:
![img64](assets/img/13.12.PNG)
<br>

- Juga berikut
![img65](assets/img/13.13.PNG)
<br>

- Untuk mencobanya, akses ``http://localhost:8080/artikel``, kemudian tambah menjadi ``http://localhost:8080/admin/artikel`` lalu tekan enter.
![img66](assets/img/13.14.png)
<br>

- Otomatis akan dialihkan untuk login terlebih dahulu.

- Mencoba masuk dengan email `admin@email.com`, dan password `admin123`, kemudian tekan `login`.
![img67](assets/img/13.15.png)
<br>

- Berhasil masuk sebagai admin, dan semua menu dapat diakses.Untuk mencobanya klik menu `Artikel`.
![img69](assets/img/13.16.png)
<br>

- Kemudian klik menu `Login Admin`, untuk diarahkan ke ``http://localhost:8080/admin/artikel``.
![img70](assets/img/13.17.png)
<br>

- Maka akan masuk ke menu admin sebelumnya, tidak login ulang.
![img71](assets/img/13.18.png)
<br>

## 7. Membuat Fungsi Logout
- Menambah method logout().
- Terletak di folder `app/Controllers`, buka file `User.php`, kemudian edit menjadi berikut:
![img72](assets/img/13.19.png)
<br>

- Untuk mencobanya, klik menu `Logout`.
![img73](assets/img/13.20.png)
<br>

- Maka akan langsung diarahkan untuk login ulang, sebelum bisa mengakses menu admin.
![img74](assets/img/13.21.png)
<br>

- Namun, untuk ``http://localhost:8080/artikel`` masih dapat diakses.
![img75](assets/img/13.22.png)
<br>

</div>