# Laporan Jobsheet 2
> Ahmad Faza Alfan Fashlah
> TI - 2F / 03

## Praktikum 1 : Basic Routing 

### Route /hello
``` php 
Route::get('/hello', function () {
    return 'Hello World';
});
```
<img src="/Screenshot/1.png"><br>
> Membuat route /hello dengan Hello World sebagai hasil returnnya sehingga ketika dibrowse menampilkan Hello Word

<br>

### Route /world
``` php 
Route::get('/world', function () {
    return 'World';
});
```
<img src="/Screenshot/2.png"><br>
> Membuat route /world dengan World sebagai hasil returnnya sehingga ketika dibrowse menampilkan World


### Route /
``` php 
Route::get('/', function () {
    return 'Selamat Datang';
});
```
<img src="/Screenshot/3.png"><br>


### Route /about
``` php 
Route::get('/about', function () {
    return ' NAME : Ahmad Faza Alfan Fashlah <br> NIM : 2241720186';
});
```
<img src="/Screenshot/4.png"><br>

## Praktikum 2 : Route Parameters 

### Route /user/Faza
``` php 
Route::get('/user/{name}', function ($name) {
    return 'Nama saya ' . $name;
});
```
<img src="/Screenshot/5.png"><br>
>Pada saat di browse maka web akan menampilkan nilai sesuai dengan $name yang menjadi parameternya 

<br>

### Route /user
<img src="/Screenshot/6.png"><br> 
> Terdapat tulisan 404 Not Found hal tersebut  terjadi karena routing yang sebelumnya dibuat adalah /user/{name} sehingga routing /user akan memunculkan 404 Not Found karena routingnya belum dibuat  

<br>

### Route /posts/2/comments/7
``` php 
Route::get('/posts/{post}/comments/{comment}', function ($postId, $commentId) {
    return 'Pos ke-' . $postId . " Komentar ke-: " . $commentId;
});
```
<img src="/Screenshot/7.png"><br> 
> Menampilkan hasil sesuai dengan parameter post dan comment yang ditulis saat melakukan browse

<br>

### Route/article/3
``` php 
Route::get('/articles/{id}', function ($id) {
    return " Halaman Artikel dengan ID " . $id;
});
```
<img src="/Screenshot/8.png"><br> 

## Praktikum 3 : Optional Parameters 
### Route /user
``` php
Route::get('/user/{name?}', function ($name = null) {
    return 'Nama saya ' . $name;
});
```
<img src="/Screenshot/9.png"><br> 
> '$name' bernilai null sehingga jika melakukan browse /user saja tidak masalah karena nilai akan otomatis menjadi nilai default yaitu null

<br>

### Route /user/Faza
``` php
Route::get('/user/{name?}', function ($name = 'John') {
    return 'Nama saya ' . $name;
});
```
<img src="/Screenshot/10.png"><br> 
>url /Faza memberikan parameter ke dalam routenya sehingga terdapat penambahan 'Faza' pada tampilan webnya

### Route/user
``` php
Route::get('/user/{name?}', function ($name = 'John') {
    return 'Nama saya ' . $name;
});
```
<img src="/Screenshot/11.png"><br> 
> web akan otomatis menampilkan nilai default yaitu 'John' saat nilai '$name" tidak diisi

<br>

## Praktikum 4 : Membuat Controller 
### Welcome Controller 
``` php
class WelcomeController extends Controller
{
    public function hello()
    {
        return 'Hello World';
    }
}
```
<img src="/Screenshot/12.png"><br>

### Home Controller 
``` php
class HomeController extends Controller
{
    public function index() {   
        return 'Selamat Datang';
    }
}
```
<img src="/Screenshot/13.png"><br>

### About Controller 
``` php
class AboutController extends Controller
{
    public function about()
    {
        return '2241720186 - Ahmad Faza Alfan Fashlah';
    }
}
```
<img src="/Screenshot/14.png"><br>

### Article Controller 
``` php
class ArticleController extends Controller
{
    public function articles($articleId) {
        return 'Halaman Artikel dengan ID '.$articleId;
    }
}
```
<img src="/Screenshot/15.png"><br>

## Praktikum 5 : Resource Controller
### PhotoController
``` php
class PhotoController extends Controller
{
    /**
     * Display a listing of the resource.
     */
    public function index()
    {
        //
    }

    /**
     * Show the form for creating a new resource.
     */
    public function create()
    {
        //
    }

    /**
     * Store a newly created resource in storage.
     */
    public function store(Request $request)
    {
        //
    }

    /**
     * Display the specified resource.
     */
    public function show(string $id)
    {
        //
    }

    /**
     * Show the form for editing the specified resource.
     */
    public function edit(string $id)
    {
        //
    }

    /**
     * Update the specified resource in storage.
     */
    public function update(Request $request, string $id)
    {
        //
    }

    /**
     * Remove the specified resource from storage.
     */
    public function destroy(string $id)
    {
        //
    }
}
```

### Web.php
``` php 
use App\Http\Controllers\PhotoController;

Route::resource('photos', PhotoController::class)->only([
    'index', 'show'
]);

Route::resource('photos', PhotoController::class)->except([
    'create', 'store', 'update', 'destroy'
]);
```
<img src="/Screenshot/16.png"><br>

## Praktikum 6 : Membuat View
### hello.blade.php
``` php
<html>
    <body>
        <h1>Hello, {{ $name }}</h1>
    </body>
</html>
```
### Web.php
``` php
Route::get('/greeting', function () {
    return view('hello', ['name' => 'Faza']);
});
```
<img src="/Screenshot/17.png"><br>
> Saat melakukan browse /greeting view hello.blade.php akan dijalankan serta menampilakan nilai sesuai dengan parameter '$name' yaitu Faza

## Praktikum 7 : View dalam Direktori 
### hello.blade.php
``` php
<html>
    <body>
        <h1>Hello, {{ $name }}</h1>
    </body>
</html>
```
### Web.php
``` php
Route::get('/greeting', function () {
    return view('blog.hello', ['name' => 'Faza']);
});
```
<img src="/Screenshot/17.png"><br>
> Mirip dengan praktikum 6, yang membedakan hanya lah ketika dipanggil di web.php maka harus ditambahkan 'blog.' terlebih dahulu

## Praktikum 8 : Menampilkan View dalam Controller
### WelcomeController.php
``` php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

class WelcomeController extends Controller
{
    public function hello()
    {
        return 'Hello World';
    }

    public function greeting()
    {
        return view('blog.hello', ['name' => 'Faza']);
    }
}
```
### Web.php
``` php
use App\Http\Controllers\WelcomeController;

Route::get('/greeting', [WelcomeController::class, 'greeting']);
```
<img src="/Screenshot/17.png"><br>
> Memindahkan panggilan view 'blog.hello' yang awalnya ada di web.php ke dalam method greeting di WelcomeController. Hal ini membuat kode lebih terstruktur dan mudah dikelola, tanpa mengubah hasil akhirnya.

## Praktikum 9 : Meneruskan Data ke View 
### WelcomeController.php
``` php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

class WelcomeController extends Controller
{
    public function hello()
    {
        return 'Hello World';
    }

    public function greeting(){
        return view('blog.hello')
            ->with('name', 'Faza')
            ->with('occupation', 'Astronout');
    }
}
```
### hello.blade.php
``` php
<html>
    <body>
         <h1>Hello, {{ $name }}</h1>
         <h1>You are {{ $occupation }}</h1>
    </body>
</html>
```

### web.php
``` php
use App\Http\Controllers\WelcomeController;

Route::get('/greeting', [WelcomeController::class, 'greeting']);
```
<img src="/Screenshot/18.png"><br>
> Controller tersebut memiliki dua method, yaitu hello() dan greeting(). Method hello() sederhana, hanya mengembalikan string 'Hello World'. Sedangkan method greeting() mengembalikan sebuah view dengan nama 'blog.hello' dan meneruskan data nama ('Faza') dan pekerjaan ('Astronout'). Di dalam view tersebut, pesan 'Hello, [name]' dan 'You are [occuupation]' ditampilkan menggunakan variabel yang diterima dari controller.