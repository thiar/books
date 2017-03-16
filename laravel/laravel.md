# Laravel

### Prasyarat dan instalasi
 - download xampp
 - download composer
 - `composer create-project --prefer-dist laravel/laravel mintegra` pada C:\xampp\htdocs
 - `cp .env.example .env`
 - `php artisan key:generate`
 - buat database di phpmyadmin, sesuaikan nama database, username dan password dengan yang di `.env`


### Struktur dan direktori
 - **app**
   - Console
   - Events
   - Exceptions
   - **Http**
     - **Controllers**
     - **Middleware** (filtering HTTP requests)
   - Jobs
   - Listeners
   - Mail
   - Notifications
   - Policies
   - Providers
 - bootstrap
 - **config**
 - **database**
   - **migrations** (definisi tabel)
   - **seeds** (inisialisasi data)
 - **public** (untuk aset html)
 - **resources**
   - assets
   - lang
   - **views**
 - **routes** (tempat menyimpan rute atau link yang bisa diakses)
 - storage
 - tests
 - **vendor**

-------------------------

### Studi kasus
Bikin aplikasi FRS. Ada proses login. Ada proses membuat matakuliah. Ada proses membuat kelas. Ada proses mahasiswa melakukan FRS.

#### Bikin design databasenya seperti pada PDM.
[PDM]
  1. Buka `database/migrations/create_users_table`. Tambahkan nrp dan role. (?)
  2. Buat model dan migration baru `php artisan make:model -m MataKuliah`. Lakukan hal yang sama untuk tabel Frs.
  3. Jalankan `php artisan migrate` untuk membuat database yang sudah dibuat di migration.
  3. Buat `database/seeds/UsersTableSeeder`. Tambahkan 3 mahasiswa dan 1 admin (dengan nrp 0).
  4. Buat seeder untuk tabel matakuliah. `php artisan make:seeder MataKuliahTableSeeder`.
  4. Buka `database/seeds/DatabaseSeeder`, uncomment bagian `UsersTableSeeder`. Tambahkan juga untuk seeder matakuliah. 
  5. Lalu jalankan `php artisan db:seed`.

### Routes dan Controller
Routes `routes/web.php` berisi list url dan controller yang menangani. Sedangkan controller berisi kode backend.
  1. `php artisan make:controller AuthController`.
  2. Buat url nya dulu di routes, untuk get dan post.
  3. Buat fungsi di controllernya untuk meload view dari login.
  4. Buat view nya. Kasih kodingan view yg udah ada. https://almsaeedstudio.com/preview > Examples > login.
  5. Buat fungsi di controllernya untuk menangkap proses login.

### Blade dan templating
  1. Download template dari AdminLTE. https://almsaeedstudio.com/preview > Documentation > Download, dan download layout dari starter page yg ada di tip.
  2. Copy templatenya ke `resources/views/layouts/main.blade.php`.
  3. Pada bagian content, hapus lalu ubah jadi `@yield('content')`.
  4. (optional) tepat diatas bagian `</head>`, tambahakan `@yield('css')`.
  5. (optional) tepat diatas bagian `</html>`, tambahakan `@yield('js')`.

### Basic CRUD dari tiap tabel
  1. Jalankan `php artisan make:controller -r MataKuliahController`.
  2. Jelaskan maksud dari masing masing fungsi pada MataKuliahController.
  3. Buat fungsi index beserta view nya.
  4. Buat tombol create, mengarahkan ke fungsi create.
  5. Buat tampilan create matakuliah beserta fungsi store nya.
  6. Buat juga view dan create untuk Mahasiswa.

### Proses FRS
  1. Buat menu FRS.
  2. Buat view untuk menampilkan proses FRS. Ada tabel matakuliah yang sedang diambil, ada dropdown untuk mengambil matakuliah.