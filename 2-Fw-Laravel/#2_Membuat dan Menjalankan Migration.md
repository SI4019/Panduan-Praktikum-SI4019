Halo teman-teman semuanya, di praktikum sebelumnya kita sudah berhasil menginstall dan menjalankan project dengan Laravel 8, dan pada kesempatan kali ini kita semua akan belajar bagaimana cara membuat `migration` dan menjalankan `migration`.

`Migration` adalah sebuah version control database, dimana akan membantu team untuk mengubah dan membagikan sebuah schema database dari aplikasi yang dibangun. Jika sebelumnya teman-teman biasanya membuat table-table secara manual di dalam database, maka dengan migration hal itu sudah tidak perlu dilakukan lagi.

Pada kesempatan kali ini kita akan belajar membuat migration baru, yang mana ini akan kita gunakan untuk studi kasus membuat CRUD di Laravel 8. Langsung saja kita mulai.

## Langkah 1 - Koneksi Database

Pertama, silahkan buka file `.env `dan kemudian silahkan cari kode berikut ini :

```Apache
DB_DATABASE=laravel
DB_USERNAME=root
DB_PASSWORD=
```

Dan ubahlah menjadi seperti berikut ini :

```Apache
DB_DATABASE=db_pabweblaravel8
DB_USERNAME=root
DB_PASSWORD=
```

Di atas untuk nama database yang akan kita gunakan adalah `db_pabweblaravel8` dan untuk `password` silahkan disesuaikan dengan konfigurasi MySQL dari komputer masing-masing, jika menggunakan `XAMPP` maka secara default adalah kosong atau tidak perlu diisi.

Sekarang kita lanjutkan untuk membuat database baru di dalam http://localhost/phpmyadmin dan silahkan buat database baru dengan nama `db_pabweblaravel8.`

**CATATAN!**: pastikan setelah melakukan perubahan di dalam file `.env`, untuk selelau melakukan restart server Laravel untuk melihat perubahannya.

# Langkah 2 - Membuat Model & Migration

Silahkan jalankan perintah berikut ini di dalam terminal/CMD dan tentu saja di dalam project Laravel yang sudah kita buat sebelumnya: _(Gunakan Vscode agar lebih mudah)_

```Apache
php artisan make:model Blog -m
```

![vscode](assets/img/Screen%20Shot%202021-05-28%20at%201.56.09%20PM.png)

kurang lebih seperti ini outputnya:

![migrate](assets/img/Screen%20Shot%202021-05-29%20at%201.06.58%20PM.png)

Perintah di atas akan membuat sebuah model baru dengan nama `Blog` di dalam folder `app/Models/Blog.php` dan kita juga menambahkan flag `-m` yang artinya sekaligus membuat untuk file migrationnya. Kita bisa melihatnya di `database/migrations/2021_05_29_060448_create_blogs_table.php`. Untuk nama file depan dari migration akan random sesuai dengan tanggal saat dibuat.

## Langkah 3 - Membuat Field Table Migration

Sekarang kita lanjutkan untuk menambahkan beberapa filed yang akan kita gunakan nanti, silahkan buka file `database/migrations/2021_05_29_060448_create_blogs_table.php` dan silahkan ubah pada `function up` menjadi seperti berikut ini :

```php
public function up()
{
  Schema::create('blogs', function (Blueprint $table) {
      $table->id();
      $table->string('image');
      $table->string('title');
      $table->text('content');
      $table->timestamps();
  });
}
```

Di atas kita menambahkan `3 filed` baru, yaitu `image` dengan tipe data `string`, kemudian `title` dengan tipe data `string` juga dan yang terakhir ada `content` dengan tipe data `text`.

## Langkah 4 - Menjalankan Migration

Setelah kita berhasil membuat beberapa field di dalam file migration blog, maka sekarang kita bisa mencoba menjalankan migration tersebut agar menjadi sebuah table di dalam database. Silahkan jalankan perintah di bawah ini :

```Apache
php artisan migrate
```

![migration](assets/img/Screen%20Shot%202021-05-29%20at%202.00.32%20PM.png)

Jika berhasil maka teman-teman bisa mencoba cek database dan teman-teman akan menemukan `table blog `yang sudah kita buat di dalam file migration.

![db](assets/img/Screen%20Shot%202021-05-29%20at%202.02.40%20PM.png)

## Langkah 5 - Menambahkan Mass Assigment

Sekarang kita lanjutkan untuk menambahkan `mass assigment` di dalam model Blog. Mass Assigment merupakan method yang digunakan untuk mengizinkan sebuah field dari table agar dapat menyimpan sebuah data. Kita bisa membuat mass assignment dengan properti `$fillable` di dalam model `Blog`. Silahkan buka file `app/Models/Blog.php` kemudian tambahkan kode berikut ini :

```Php
/**
* fillable
*
* @var array
*/
protected $fillable = [
    'image', 'title', 'content'
];
```

Di atas kita menambahkan `3 field`yang kita izinkan untuk menyimpan data di dalam table blogs, yaitu `images`, `title` dan `content`. Jika file model Blog di tulis dengan lengkap kurang lebih seperti berikut ini :

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class Blog extends Model
{
    use HasFactory;

    /**
     * fillable
     *
     * @var array
     */
    protected $fillable = [
        'image', 'title', 'content'
    ];
}
```

Di praktikum selanjutnya kita akan belajar bagaimana cara menampilkan data dari database di Laravel 8 dan untuk tampilannya kita nanti akan menggunakan **Framework Bootstrap secara CDN atau online**.


