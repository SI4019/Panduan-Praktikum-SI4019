![image](assets/img/4.png)

Halo teman-teman semuanya, di praktikum sebelumnya kita sudah berhasil menampilkan data dari database di layar broswer menggunakan Laravel 8, sekarang kita akan lanjutkan untuk belajar bagaimana cara melakukan insert data ke dalam database di Laravel 8. Langsung saja kita mulai.

## Langkah 1 - Membuat Function Create dan Store

Disini kita akan menambahkan `2 method/function` baru di dalam controller blog, method ini akan kita gunakan untuk proses melakukan insert data ke dalam database. Silahkan buka file a`pp/Http/Controllers/BlogController.php` dan kemudian silahkan tambahkan kode berikut ini di bawah f`unction index.`

```php
/**
* create
*
* @return void
*/
public function create()
{
    return view('blog.create');
}


/**
* store
*
* @param  mixed $request
* @return void
*/
public function store(Request $request)
{
    $this->validate($request, [
        'image'     => 'required|image|mimes:png,jpg,jpeg',
        'title'     => 'required',
        'content'   => 'required'
    ]);

    //upload image
    $image = $request->file('image');
    $image->storeAs('public/blogs', $image->hashName());

    $blog = Blog::create([
        'image'     => $image->hashName(),
        'title'     => $request->title,
        'content'   => $request->content
    ]);

    if($blog){
        //redirect dengan pesan sukses
        return redirect()->route('blog.index')->with(['success' => 'Data Berhasil Disimpan!']);
    }else{
        //redirect dengan pesan error
        return redirect()->route('blog.index')->with(['error' => 'Data Gagal Disimpan!']);
    }
}

```

Di atas kita menambahkan `2 function baru`, yaitu :

- `create`
- `store`

### function create

`Function create` akan kita gunakan untuk menampilkan form, dimana form ini akan digunakan oleh user untuk melakukan input data, seperti memasukkan data tiltle, content dan gambar.

### function store

`Function store` akan digunakan untuk melakukan proses insert data ke dalam database, di dalam function store kita membuat sebuah validasi, dimana data akan di masukkan ke dalam database jika validasi tersebut sudah terpenuhi. Beirkut ini beberapa validasi yang akan digunakan saat menambahkan data ke dalam database.

```php
$this->validate($request, [
   'image'     => 'required|image|mimes:png,jpg,jpeg',
   'title'     => 'required',
   'content'   => 'required'
]);
```

Di atas untuk filed `image` kita buat validasi dengan `required`, yang artinya filed image ini wajib diisi, kemudian diikuti dengan `image` yang artinya file yang di upload harus berupa gambar dan yang terakhir adalah `mimes`, dimana mimes ini adalah extension dari file gambar yang di upload, yaitu png, jpg dan jpeg.

Kemudian untuk field `title` kita hanya buat `required`, yang artinya harus wajiib diisi. Dan untuk `content` juga sama, kita menggunakan validasi `required`, yang artinya wajib diisi.

Jika validasi di atas terpenuhi, maka akan melakukan insert data ke dalam database dan melaukan upload gambar ke dalam server. Kurang lebih menggunakan kode seperti berikut ini :

```php
//upload image
$image = $request->file('image');
$image->storeAs('public/blogs', $image->hashName());

$blog = Blog::create([
   'image'     => $image->hashName(),
   'title'     => $request->title,
   'content'   => $request->content
]);
```

Di atas untuk gambar yang akan diupload ke server, akan di letakkan di dalam folder `storage/app/public/blogs/` dan untuk nama file yang diupload akan otomatis direname menjadi random dengan method `hashName().`
Kemudian di bawahnya kita membuat sebuah kondisi dimana apabila variable `$blog` bernilai true yang artinya data berhasil di insert ke database, maka akan membuat sebuah session dengan nama key `success` dan valuenya adalah data berhasil disimpan!.

Dan jika `$blog `bernilai `false` atau data gagal di insert ke dalam database, maka akan membuat session dengan key `error` dan valuenya adalah data gagal disimpan!.

Kemudian akan di redirect ke sebuah route dengan nama blog.index dengan membahwa session di atas. Kurang lebih seperti berikut ini :

```php
if($blog){
  //redirect dengan pesan sukses
  return redirect()->route('blog.index')->with(['success' => 'Data Berhasil Disimpan!']);
}else{
  //redirect dengan pesan error
  return redirect()->route('blog.index')->with(['error' => 'Data Gagal Disimpan!']);
}
```

## Langkah 2 - Membuat View Create

Setelah kita berhasil menambahkan `2 function baru` untuk proses insert data, sekarang kita lanjutkan untuk membuat halaman view atau templatenya. Silahkan buat file baru dengan nama `create.blade.php` di dalam folder `resources/views/blog` dan masukkan kode berikut ini :

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Tambah Data Blog - Pabweblaravel</title>
    <link
      rel="stylesheet"
      href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css"
    />
  </head>
  <body style="background: lightgray">
    <div class="container mt-5 mb-5">
      <div class="row">
        <div class="col-md-12">
          <div class="card border-0 shadow rounded">
            <div class="card-body">
              <form
                action="{{ route('blog.store') }}"
                method="POST"
                enctype="multipart/form-data"
              >
                @csrf

                <div class="form-group">
                  <label class="font-weight-bold">GAMBAR</label>
                  <input
                    type="file"
                    class="form-control @error('image') is-invalid @enderror"
                    name="image"
                  />

                  <!-- error message untuk title -->
                  @error('image')
                  <div class="alert alert-danger mt-2">{{ $message }}</div>
                  @enderror
                </div>

                <div class="form-group">
                  <label class="font-weight-bold">JUDUL</label>
                  <input
                    type="text"
                    class="form-control @error('title') is-invalid @enderror"
                    name="title"
                    value="{{ old('title') }}"
                    placeholder="Masukkan Judul Blog"
                  />

                  <!-- error message untuk title -->
                  @error('title')
                  <div class="alert alert-danger mt-2">{{ $message }}</div>
                  @enderror
                </div>

                <div class="form-group">
                  <label class="font-weight-bold">KONTEN</label>
                  <textarea
                    class="form-control @error('content') is-invalid @enderror"
                    name="content"
                    rows="5"
                    placeholder="Masukkan Konten Blog"
                  >
{{ old('content') }}</textarea
                  >

                  <!-- error message untuk content -->
                  @error('content')
                  <div class="alert alert-danger mt-2">{{ $message }}</div>
                  @enderror
                </div>

                <button type="submit" class="btn btn-md btn-primary">
                  SIMPAN
                </button>
                <button type="reset" class="btn btn-md btn-warning">
                  RESET
                </button>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js"></script>
    <script src="https://cdn.ckeditor.com/4.13.1/standard/ckeditor.js"></script>
    <script>
      CKEDITOR.replace("content");
    </script>
  </body>
</html>
```

Di atas untuk form akan kita arahkan ke sebuah route yang bernama `blog.store,` dimana route ini akan menuju ke sebuah `function store` yang berada di dalam `controller blog.`

```php
<form action="{{ route('blog.store') }}" method="POST" enctype="multipart/form-data">
```

Dan jangan lupa!, jika kita membuat sebuah form dengan upload sebuah berkas, entash itu file ataupun gambar, jangan lupa untuk menyertakan attribute `enctype="multipart/form-data”`. Jika tidak, maka proses upload file tidak akan bekerja.

Kemudian untuk konten blog, kita akan replace textarea dengan nama `content` menggunakan `CKEDITOR`, kurang lebih seperti berikut ini :

```php
<script src="https://cdn.ckeditor.com/4.13.1/standard/ckeditor.js"></script>
<script>
    CKEDITOR.replace( 'content' );
</script>
```

## Langkah 3 - Menjalankan Project

Sekarang kita bisa mencoba menjalankan projectnya di http://localhost:8000/blog/create atau bisa dengan menekan tombol tambah blog di atas table. Dan jika berhasil maka kurang lebih tampilannya seperti berikut ini :

![4](assets/img/Screen%20Shot%202021-05-30%20at%209.36.51%20PM.png)

Sekarang kita coba klik button `SIMPAN` tanpa mengisikan data apapun di dalam inputan, maka kurang lebih hasilnya akan seperti berikut ini :

![5](assets/img/Screen%20Shot%202021-05-30%20at%209.39.10%20PM.png)

Di atas akan menampilkan sebuah `validasi error`, karena diatas kita tidak memasukkan data apapaun saat proses `SIMPAN` data. Sekarang kita bisa coba untuk memasukkan data ke form tersebut dan klik `SIMPAN`. Jika berhasil kita akan mendapatkan tampilan seperti berikut ini :

![4](assets/img/Screen%20Shot%202021-05-30%20at%2011.21.49%20PM.png)

Bagaimana ? mudah bukan cara memasukkan data ke dalam database menggunakan Laravel 8 dan Bootstrap. Di praktikum selanjutnya kita semua akan belajar bagaimana cara meng-edit data kemudian meng-updatenya ke dalam database di Laravel 8.



