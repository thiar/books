# Laravel

### Prasyarat dan instalasi
 - `composer create-project --prefer-dist laravel/laravel blog`
 - `cp .env.example .env`
 - `php artisan key:generate`
 - buat database di phpmyadmin, sesuaikan namanya dengan yang di `.env`


### Struktur dan direktori
 - app
   - ~~Console~~
   - ~~Events~~
   - ~~Exceptions~~
   - Http
     - Controllers
     - Middleware
   - ~~Jobs~~
   - ~~Listeners~~
   - ~~Mail~~
   - ~~Notifications~~
   - ~~Policies~~
   - ~~Providers~~
 - ~~bootstrap~~
 - config
 - database
 - public
 - resources
 - routes
 - ~~storage~~
 - ~~tests~~
 - vendor

### ~~Alur~~

#### ./public/index.php
File ini adalah titik masuk dari semua request, yang diarahkan oleh webserver. 
File ini tidak berisi banyak kode, namun hanyalah awal untuk meload framework laravel.

#### Kernels
Selanjutnya, request diarahkan ke `app/Http/Kernel.php`. Kernel ini menyiapkan error handling, logging, application environment, middleware, dan lain lain. Intinya nyiapin dasar frameworknya.

#### Service providers
Semua service providers yang dikonfigurasi di `config/app.php` pada array `providers` akan diload.
Lalu pada `app/Providers/AppServiceProviders`, fungsi `register` dijalankan untuk menambah service lain, fungsi `boot` dijalankan untuk menjalankan service lain.

#### Dispatch request
Setelah aplikasi sudah siap, request akan ditangani oleh `routes/web.php`. Dari router tersebut, request akan diproses oleh controller, middleware, atau lainnya.

### Studi kasus
Bikin aplikasi FRS blablabla. Ada proses login. Ada proses membuat matakuliah. Ada proses membuat kelas. Ada proses mahasiswa melakukan FRS.

### Routes dan Controller
Routes `routes/web.php` berisi list url dan controller yang menangani. Sedangkan controller berisi kode backend.
Kasih contoh membuat AuthController.
  1. Buka `database/migrations/create_users_table`. Tambahkan nrp dan role. (?)
  2. Jalankan `php artisan migrate` untuk membuat database users. (Sambil jelasin migrate itu apa, seeder itu apa)
  3. Buat seeder data user (role mahasiswa). Jalankan seeder.
  4. Buat url nya dulu di routes, untuk get dan post.
  5. Buat fungsi di controllernya untuk meload view dari login.
  6. Buat view nya. Kasih kodingan view yg udah ada.
  7. Buat fungsi di controllernya untuk menangkap proses login.

### Blade dan templating
  1. Download template dari AdminLTE. https://almsaeedstudio.com/preview > Documentation > Download, dan download layout dari starter page yg ada di tip.
  2. Copy templatenya ke `resources/views/layouts/main.blade.php`.
  3. Pada bagian content, hapus lalu ubah jadi `@yield('content')`.
  4. (optional) tepat diatas bagian `</head>`, tambahakan `@yield('css')`.
  5. (optional) tepat diatas bagian `</html>`, tambahakan `@yield('js')`.

