![5](assets/img/5.png)

Halo teman-teman semuanya, di praktukum sebelumnya kita sudah banyak belajar bagaimana cara melakukan `insert data ke dalam database menggunakan Laravel 8 dan Bootstrap`. Dan sekarang kita akan melanjutkan belajarnya untuk proses edit dan update data ke dalam database. Disini kita akan menambahkan `2 function/method` baru di dalam controller Blog untuk proses edit dan update data. Oke langsung saja kita mulai.

## Langkah 1 - Membuat Function Edit dan Update

Sekarang kita akan menambahkan `2 function `baru di dalam `controller blog`, ini akan kita manfaatkan untuk proses menampilkan data yang akan di edit dan melakukan update data ke dalam database. Silahkan buka file `app/Http/Controllers/BlogController.php` dan kemudian silahkan tambahkan function di bawah ini tepat di bawah `function store.`

```php
/**
* edit
*
* @param  mixed $blog
* @return void
*/
public function edit(Blog $blog)
{
    return view('blog.edit', compact('blog'));
}


/**
* update
*
* @param  mixed $request
* @param  mixed $blog
* @return void
*/
public function update(Request $request, Blog $blog)
{
    $this->validate($request, [
        'title'     => 'required',
        'content'   => 'required'
    ]);

    //get data Blog by ID
    $blog = Blog::findOrFail($blog->id);

    if($request->file('image') == "") {

        $blog->update([
            'title'     => $request->title,
            'content'   => $request->content
        ]);

    } else {

        //hapus old image
        Storage::disk('local')->delete('public/blogs/'.$blog->image);

        //upload new image
        $image = $request->file('image');
        $image->storeAs('public/blogs', $image->hashName());

        $blog->update([
            'image'     => $image->hashName(),
            'title'     => $request->title,
            'content'   => $request->content
        ]);

    }

    if($blog){
        //redirect dengan pesan sukses
        return redirect()->route('blog.index')->with(['success' => 'Data Berhasil Diupdate!']);
    }else{
        //redirect dengan pesan error
        return redirect()->route('blog.index')->with(['error' => 'Data Gagal Diupdate!']);
    }
}
```

Di atas kita membuat `2 function` untuk proses edit dan update data, yaitu :

- edit
- update

### function edit

`Function edit` digunakan untuk menampilkan data yang akan di edit ke dalam sebuah form, jika teman-teman perhatikan di dalam function ini kita memiliki sebuah parameter, yaitu `Blog $blog`, yang artinya parameter tersebut adalah model Blog yang diambil datanya sesuai dengan ID yang di dapatkan dari URL.

Setelah data tersebut di dapatkan, maka akan di parsing ke dalam `view edit.blade.php` di dalam folder `blog` dengan menggunakan helper `compact.`

```php
return view('blog.edit', compact('blog'));
```

Nah sekarang kita sudah bisa memanggil data blog berdasarkan ID yang diambil dari URL di dalam template edit. Untuk contoh memanggilnya kita bisa menggunakan sintaks seperti ini :

```Laravel
{{ $blog->title }}
```

### function update

`Function update` akan kita manfaatkan untuk melakukan update data blog ke dalam database, sebelum itu disini kita juga menambahkan sebuah validasi, dimana jika validasi tersebut terpenuhi, maka data baru akan bisa di update ke dalam database sesuai dengan ID dari data blog tersebut.

Untuk proses update data blog sendiri kita menggunakan sebuah kondisi, dimna jika tidak ada request file dengan `nama image,` maka kita hanya akan melakukan update tanpa meng-update filed image.

```php
$blog->update([
    'title' => $request->title,
    'content' => $request->content
]);
```

Dan apabila request file dengan nama `image` tersedia, artinya disini kita akan melakuakn update data image. Pertama kita akan `remove gambar` yang lama terlebih dahulu.

```php
//hapus old image
Storage::disk('local')->delete('public/blogs/'.$blog->image);
```

Setelah gambar yang lama terhapus, sekarang kita lakukan upload image baru

```php
//upload new image
$image = $request->file('image');
$image->storeAs('public/blogs', $image->hashName());
```

Dan kemudian data diupdate ke dalam database dengan filed nama image yang baru :

```php
$blog->update([
    'image' => $image->hashName(), // <— new name file image
    'title' => $request->title,
    'content' => $request->content
]);
```

## Langkah 2 - Membuat View Edit

Sekarang kita lanjutkan untuk membuat view untuk menampilkan data yang ingin kita edit dan update. Silahkan buat file baru dengan nama `edit.blade.php` di dalam folder `resources/views/blog/ `dan kemudian silahkan masukkan kode berikut ini :

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Edit Data Blog - Pabweblaravel</title>
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
                action="{{ route('blog.update', $blog->id) }}"
                method="POST"
                enctype="multipart/form-data"
              >
                @csrf @method('PUT')

                <div class="form-group">
                  <label class="font-weight-bold">GAMBAR</label>
                  <input type="file" class="form-control" name="image" />
                </div>

                <div class="form-group">
                  <label class="font-weight-bold">JUDUL</label>
                  <input
                    type="text"
                    class="form-control @error('title') is-invalid @enderror"
                    name="title"
                    value="{{ old('title', $blog->title) }}"
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
{{ old('content', $blog->content) }}</textarea
                  >

                  <!-- error message untuk content -->
                  @error('content')
                  <div class="alert alert-danger mt-2">{{ $message }}</div>
                  @enderror
                </div>

                <button type="submit" class="btn btn-md btn-primary">
                  UPDATE
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

Untuk action dari form kita akan arahkan ke sebuah route `blog.update,` dengan parameter `ID` dari data blog, yaitu :

```php
<form action="{{ route('blog.update', $blog->id) }}" method="POST" enctype="multipart/form-data">
```

kemudian jangan lupa, jika kita membuat sebuah edit data, pastikan telah menambahkan method `PUT` di dalam form, kurang lebih seperti berikut ini :

```php
@method('PUT')
```

Dan untuk menampilkan data di dalam form, kita menggunakan helper `old`, kurang lebih contohnya seperti berikut ini :

```php
<input type="text" class="form-control @error('title') is-invalid @enderror" name="title" value="{{ old('title', $blog->title) }}" placeholder="Masukkan Judul Blog">
```
### Langkah 3 - Menjalankan Project

Sekarang kita bisa mencoba menjalankan projectnya, dengan cara klik tombol edit di dalam table data, dan jika berhasil kurang lebih seperti berikut ini :

![5](assets/img/Screen%20Shot%202021-05-30%20at%2011.29.00%20PM.png)

Dan kita coba edit datanya dan kita `klik UPDATE,` maka jika berhasil kurang lebih tampilannya akan seperti berikut ini :

![5](assets/img/Screen%20Shot%202021-05-30%20at%2011.31.37%20PM.png)

Di praktikum selanjutnya kita semua akan belajar bagaimana cara membuat delete data di dalam Laravel 8.

