Halo teman-teman semuanya, di praktikum sebelumnya kita sudah belajar bersama-sama tentang bagaimana cara membuat _migration_ dan _menjalankan migration di dalam Laravel 8_, pada kesempatan kali ini kita semua akan belajar bagaimana cara menampilkan data dari database menggunakan Laravel 8 dan untuk tampilannya kita menggunakan Bootstrap. Langsung saja kita mulai.

## Langkah 1 - Membuat Controller Blog

Pertama kita akan membuat controller blog terlebih dahulu, penamaan controller untuk best practice-nya di sarankan menggunakan kata singular. Untuk mengetahui tentang Best Practice di dalam Laravel, teman-teman bisa membacanya di link berikut ini: [Laravel Best Practices for Developers | 2021](https://tony-stark.medium.com/larave-best-practices-for-developers-2021-19cf662f7de8)

Silahkan jalankan perintah berikut ini untuk membuat controller blog.

```Apache
php artisan make:controller BlogController
```

Jika berhasil teman-teman akan mendapatkan 1 file baaru di dalam folder `app/Http/Controllers/BlogController.php`. Silahkan buka file tersebut kemudian ubah kode-nya menjadi seperti berikut ini :

![BlogController](assets/img/Screen%20Shot%202021-05-29%20at%202.21.26%20PM.png)

Di atas pertama kita import Model `Blog` terlebih dahulu, karena kita akan menggunakan model ini untuk menampilkan data, input data dan yang lain-nya.

```php
use App\Models\Blog;
```

Kemudian kita juga import `Http Request` dari Laravel, ini akan kita manfaatkan untuk mendapatkan data request dari sisi client untuk di masukkan di dalam database saat proses input data.

```php
use Illuminate\Http\Request;
```

Dan kita juga import `Facades Storage` dari Laravel, ini akan kita manfaatkan untuk melakukan store atau upload data gambar ke dalam server.

```php
use Illuminate\Support\Facades\Storage;
```

Kemudian di atas kita menambahkan `1 method/function` baru yaitu `index`, ini akan kita manfaatkan untuk menampilkan data blog di dalam project kita.

Di dalam `function index` kita memanggil Model Blog kemudian mengurutkan datanya berdasarkan terbaru dengan method `latest()` dan membatasi data yang ditampilkan sejumlah 10 data perhalaman.

```php
$blogs = Blog::latest()->paginate(10);
```

Setelah itu kita memanggil sebuah view dengan nama `index.blade.php` di dalam folder blog yang mana folder tersebut berada di dalam folder `resources/views/`. Dan kita parsing data blog tersebut ke dalam view menggunakan helper `compact`.

```php
return view('blog.index', compact('blogs'));
```

## Langkah 2 - Konfigurasi Namespace Route

Di dalam Laravel 8 untuk proses pembuatan route akan sedikit berbeda dengan versi-versi laravel sebelumnya, dimana untuk konfigurasi `namespace` akan di set ke `null`, yang artinya jika kita ingin membuat route baru, harus melakukan import `namespace` di dalam file `routes/web.php.`

Akan tetapi kita juga bisa mengaturnya agar tidak harus melakukan import namespace di dalam file route, langsung saja kita mulai. Silahkan buka file `app/Providers/RouteServiceProvider.php` kemudian cari kode berikut ini :

```php
protected $namespace = null;
```

Kemudian ganti menjadi seperti berikut ini :

```php
protected $namespace = 'App\Http\Controllers';
```

Di atas kita membuat agar namespace dari controller kita arahkan ke dalam folder `app/Http/Controllers`. Dan setelah itu kita juga harus melakukan register `namespace` di dalam method `boot`.

```php
public function boot()
{
  $this->configureRateLimiting();

  $this->routes(function () {
      Route::middleware('web')
        ->namespace($this->namespace) // <— tambahkan ini
        ->group(base_path('routes/web.php'));


      Route::prefix('api')
        ->namespace($this->namespace) // <— tambahkan ini
        ->middleware('api')
        ->group(base_path('routes/api.php'));
 });
}
```

## Langkah 3 - Membuat Route

Setelah kita belajar konfigurasi route untuk default namespacenya, maka sekarang kita bisa membuat route utuk blog controller. Silahkan buka file `routes/web.php` kemudian tambahkan kode berikut ini :

```php
Route::resource('blog', BlogController::class);
```

Di atas kita menggunakan route dengan jenis `resources`, yang artinya route tersebut sudah complete, mulai dari `index`, `create`, `store`, `edit`, `update` dan `destroy`. Jadi kita tidak perlu define route satu-satu. Jika kita coba jalankan perintah di bawah ini maka teman-teman bisa melihatnya.

```Apache
php artisan route:list
```
![routeresource](assets/img/Screen%20Shot%202021-05-29%20at%202.59.51%20PM.png)

## Langkah 4 - Membuat View

Setelah kita berhasil menambahkan route, sekarang kita lanjutkan untuk membuat view untuk menampilkan data blog di layar browser. Silahkan buat folder baru dengan nama `blog` di dalam folder `resources/views/` dan kemudian di dalam folder `blog` silahkan buat file baru dengan nama `index.blade.php`dan massukkan kode berikut ini :

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Data Blogs - pabweblaravel</title>
    <link
      rel="stylesheet"
      href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css"
    />
    <link
      rel="stylesheet"
      href="//cdnjs.cloudflare.com/ajax/libs/toastr.js/latest/toastr.min.css"
    />
  </head>
  <body style="background: lightgray">
    <div class="container mt-5">
      <div class="row">
        <div class="col-md-12">
          <div class="card border-0 shadow rounded">
            <div class="card-body">
              <a
                href="{{ route('blog.create') }}"
                class="btn btn-md btn-success mb-3"
                >TAMBAH BLOG</a
              >
              <table class="table table-bordered">
                <thead>
                  <tr>
                    <th scope="col">GAMBAR</th>
                    <th scope="col">JUDUL</th>
                    <th scope="col">CONTENT</th>
                    <th scope="col">AKSI</th>
                  </tr>
                </thead>
                <tbody>
                  @forelse ($blogs as $blog)
                  <tr>
                    <td class="text-center">
                      <img
                        src="{{ Storage::url('public/blogs/').$blog->image }}"
                        class="rounded"
                        style="width: 150px"
                      />
                    </td>
                    <td>{{ $blog->title }}</td>
                    <td>{!! $blog->content !!}</td>
                    <td class="text-center">
                      <form
                        onsubmit="return confirm('Apakah Anda Yakin ?');"
                        action="{{ route('blog.destroy', $blog->id) }}"
                        method="POST"
                      >
                        <a
                          href="{{ route('blog.edit', $blog->id) }}"
                          class="btn btn-sm btn-primary"
                          >EDIT</a
                        >
                        @csrf @method('DELETE')
                        <button type="submit" class="btn btn-sm btn-danger">
                          HAPUS
                        </button>
                      </form>
                    </td>
                  </tr>
                  @empty
                  <div class="alert alert-danger">
                    Data Blog belum Tersedia.
                  </div>
                  @endforelse
                </tbody>
              </table>
              {{ $blogs->links() }}
            </div>
          </div>
        </div>
      </div>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js"></script>
    <script src="//cdnjs.cloudflare.com/ajax/libs/toastr.js/latest/toastr.min.js"></script>

    <script>
      //message with toastr
      @if(session()->has('success'))

          toastr.success('{{ session('success') }}', 'BERHASIL!');

      @elseif(session()->has('error'))

          toastr.error('{{ session('error') }}', 'GAGAL!');

      @endif
    </script>
  </body>
</html>
```

Di atas untuk menampilkan data blog kita menggunakan perulangan `forelse`, dimana kita bisa melakukan perulangan data jika ada tersebut tersedia dan jika data tidak ada maka akan menampilkan message bahwa data belum tersedia, kurang lebih seperti berikut ini :

```php
@forelse ($blogs as $blog)

    //perulangan data blog

@empty

    <div class="alert alert-danger">
      Data Blog belum Tersedia.
    </div>

@endforelse
```

Kemudian untuk menampilkan alert setelah kita berhasil menambahkan data, disini kita menggunakan library [Toastr](https://github.com/CodeSeven/toastr), untuk menampilkannya kurang lebih seperti berikut ini :

```php
<script>
  //message with toastr
  @if(session()->has('success'))

     toastr.success('{{ session('success') }}', 'BERHASIL!');

  @elseif(session()->has('error'))

     toastr.error('{{ session('error') }}', 'GAGAL!');

  @endif
</script>
```

Alert ini bisa kita lihat saat kita berhasil atau gagal melakukan input data, update data dan hapus data.

Dan untuk menampilkan image dari post, di atas kita menggunaka kode seperti berikut ini :

```php
<img src="{{ Storage::url('public/blogs/').$blog->image }}" class="rounded" style="width: 150px">
```
## Langkah 5 - Menjalankan Project

Sekarang kita bisa mencoba menjalankan projectnya di http://localhost:8000/blog dan jika berhasil kurang lebih tampilannya seperti berikut ini :

![datablog](assets/img/Screen%20Shot%202021-05-29%20at%203.30.56%20PM.png)

Di atas kita sudah berhasil menampilkan data dari database, message itu muncul karena kita belum memiliki data apapun di dalam table blogs, di praktikum selanjutnya kita semua akan belajar bagaimana cara insert data ke dalam database di Laravel 8.

