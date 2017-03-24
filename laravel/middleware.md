# Laravel

### Middleware

> Middleware provide a convenient mechanism for dealing with HTTP requests entering your application (before middleware), or responses leaving it (after middleware).

#### Lokasi penting
 - `app\Http\Kernel.php` pada `$routeMiddleware` menyimpan nama singkat middleware.
 - `app\Http\Middleware` menyimpan middleware yang akan digunakan oleh user.

#### Log middleware
 - `php artisan make:middleware AccessLogMiddleware`.
 - Buka middleware yang baru dibuat, buat kode untuk memasukkan log model AccessLog.
 - Tambahkan rute middleware tersebut di kernel dengan nama `access-log`.
 - Tambahkan controller yang menampilkan jumlah halaman diakses.
 - Tambahkan rute controller tersebut, menggunakan middleware.

#### Auth middleware
  Laravel menyediakan middleware authentikasi user, yaitu user harus melakukan login untuk mengakses rute tertentu. 
  Untuk menggunakan fungsi-fungsi yang berkaitan dengan Auth, masukkan `use Auth` pada controller.

#### Entrust
##### Set up
 1. Pada `config/app.php`, tambahkan
   - `Zizaco\Entrust\EntrustServiceProvider::class,` pada `'providers'`
   - `'Entrust'   => Zizaco\Entrust\EntrustFacade::class,` pada `'aliases'`

 2. Pada `app/Http/Kernel.php`, tambahkan pada `$routeMiddleware`
  ```php
  'role' => \Zizaco\Entrust\Middleware\EntrustRole::class,
  'permission' => \Zizaco\Entrust\Middleware\EntrustPermission::class,
  'ability' => \Zizaco\Entrust\Middleware\EntrustAbility::class,
```

 3. Jalankan `php artisan entrust:migration` untuk membuat tabel khusus entrust.

 4. Buat file baru `app/Role.php` dengan `php artisan make:model Role`, lalu isi dengan
  ```php
<?php

namespace App;

use Zizaco\Entrust\EntrustRole;

class Role extends EntrustRole
{
}
```

 5. Buat file baru `app/Permission.php` dengan `php artisan make:model Permission`, lalu isi dengan
  ```php
<?php

namespace App;

use Zizaco\Entrust\EntrustPermission;

class Permission extends EntrustPermission
{
}
```

 6. Lalu pada file `app/User.php`, tambahkan kode berikut
  ```php
<?php

use Zizaco\Entrust\Traits\EntrustUserTrait;

class User extends Eloquent
{
    use EntrustUserTrait; // add this trait to your user model

    ...
}
```
 7. Jalankan `composer dump-autoload`

 8. Pada `.env`, pastikan nilai `CACHE_DRIVER=array`

 9. Pada `database/seeds/DatabaseSeeder.php`, uncomment bagian RolesTableSeeder.
 10. Jalankan `php artisan migrate`, dan `php artisan db:seed`

##### Penggunaan
 - Menggunakan middleware `role:lecturer` untuk membatasi rute hanya bisa diakses oleh role lecturer.
 - Menggunakan template pada blade
```html
@permission('student')
    <p>Pesan ini hanya bisa diakses oleh student.</p>
@endpermission
```