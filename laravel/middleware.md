# Laravel

### Middleware

> Middleware provide a convenient mechanism for dealing with HTTP requests entering your application (before middleware), or responses leaving it (after middleware).

#### Lokasi penting
 - `app\Http\Kernel.php` pada `$routeMiddleware` menyimpan nama singkat middleware.
 - `app\Http\Middleware` menyimpan middleware yang akan digunakan oleh user.

#### Log middleware
 - `php artisan make:model -m AccessLog`.
 - `php artisan make:middleware AccessLogMiddleware`.
 - Buka middleware yang baru dibuat, buat kode masukin ke tabel lewat model AccessLog.
 - Tambahkan rute middleware di kernel.
 - Tambahkan controller yang berisi menampilkan jumlah halaman diakses.
 - Tambahkan rute controller tersebut, menggunakan middleware.

#### Entrust
##### Set up
 1. Pada `config/app.php`, tambahkan
   - `Zizaco\Entrust\EntrustServiceProvider::class,`
   - `'Entrust'   => Zizaco\Entrust\EntrustFacade::class,`

 2. Pada `app/Http/Kernel.php`, tambahkan
  ```php
  'role' => \Zizaco\Entrust\Middleware\EntrustRole::class,
  'permission' => \Zizaco\Entrust\Middleware\EntrustPermission::class,
  'ability' => \Zizaco\Entrust\Middleware\EntrustAbility::class,
```

 3. Jalankan `php artisan entrust:migration` untuk membuat tabel khusus entrust. Lalu jalankan `php artisan migrate`.

 4. Buat file `app/Role.php`
  ```php
<?php namespace App;

use Zizaco\Entrust\EntrustRole;

class Role extends EntrustRole
{
}
```

 5. Buat file `app/Permission.php`
  ```php
<?php namespace App;

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

 7. Terakhir, jalankan `composer dump-autoload`
