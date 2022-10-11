![cover](assets/img/1.png)

## Langkah 1 - Membuat Project Laravel Baru

Pada kesempatan kali ini kita akan belajar membuat project Laravel 8 baru menggunakan `composer` `create-project`. Dan pastikan teman-teman sudah menginstall Composer sebelumnya, jika teman-teman belum menginstallnya, silahkan bisa menginstallnya terlebih dahulu dan bisa ikuti cara installasinya melalui situs resminya di https://getcomposer.org dan silahkan disesuaikan dengan sistem operasi yang digunakan.

Untuk mengetahui apakah komputer kita sudah terinstall composer atau belum, kita bisa menjalankan perintah di bawah ini di dalam terminal/CMD.

```Apache
composer
```

Jika berhasil maka kurang lebih tampilannya seperti berikut ini :

![composer](assets/img/Screen%20Shot%202021-05-27%20at%202.03.55%20PM.png)

Sekarang kita sudah bisa membuat project laravel menggunakan composer. Silahkan masuk di dalam folder dimana teman-teman akan membuat projectnya dan jalankan perintah di bawah ini :

```Apache
composer create-project --prefer-dist laravel/laravel 21-pabweb
```
Perintah di atas akan membuat project Laravel 8 baru dengan nama `21-pabweb` dan pastikan teman-teman semuanya harus terhubung dengan internet, karena semua paket akan diunduh secara online.

Berikut prosesnya

```Apache
➜  PABWEB-LARAVEL composer create-project --prefer-dist laravel/laravel 21-pabweb
Creating a "laravel/laravel" project at "./21-pabweb"
Installing laravel/laravel (v8.5.18)
  - Downloading laravel/laravel (v8.5.18)
  - Installing laravel/laravel (v8.5.18): Extracting archive
Created project in /Volumes/ISTORAGE 1T/Repositori Praktikum Web/PABWEB-LARAVEL/21-pabweb
> @php -r "file_exists('.env') || copy('.env.example', '.env');"
Loading composer repositories with package information
Updating dependencies
Lock file operations: 104 installs, 0 updates, 0 removals
  - Locking asm89/stack-cors (v2.0.3)
  - Locking brick/math (0.9.2)
  - Locking doctrine/inflector (2.0.3)
  - Locking doctrine/instantiator (1.4.0)
  - Locking doctrine/lexer (1.2.1)
  - Locking dragonmantank/cron-expression (v3.1.0)
  - Locking egulias/email-validator (2.1.25)
  - Locking facade/flare-client-php (1.8.0)
  - Locking facade/ignition (2.9.0)
  - Locking facade/ignition-contracts (1.0.2)
  - Locking fakerphp/faker (v1.14.1)
  - Locking fideloper/proxy (4.4.1)
  - Locking filp/whoops (2.12.1)
  - Locking fruitcake/laravel-cors (v2.0.4)
  - Locking graham-campbell/result-type (v1.0.1)
  - Locking guzzlehttp/guzzle (7.3.0)
  - Locking guzzlehttp/promises (1.4.1)
  - Locking guzzlehttp/psr7 (1.8.2)
  - Locking hamcrest/hamcrest-php (v2.0.1)
  - Locking laravel/framework (v8.43.0)
  - Locking laravel/sail (v1.7.0)
  - Locking laravel/tinker (v2.6.1)
  - Locking league/commonmark (1.6.2)
  - Locking league/flysystem (1.1.3)
  - Locking league/mime-type-detection (1.7.0)
  - Locking mockery/mockery (1.4.3)
  - Locking monolog/monolog (2.2.0)
  - Locking myclabs/deep-copy (1.10.2)
  - Locking nesbot/carbon (2.48.1)
  - Locking nikic/php-parser (v4.10.5)
  - Locking nunomaduro/collision (v5.4.0)
  - Locking opis/closure (3.6.2)
  - Locking phar-io/manifest (2.0.1)
  - Locking phar-io/version (3.1.0)
  - Locking phpdocumentor/reflection-common (2.2.0)
  - Locking phpdocumentor/reflection-docblock (5.2.2)
  - Locking phpdocumentor/type-resolver (1.4.0)
  - Locking phpoption/phpoption (1.7.5)
  - Locking phpspec/prophecy (1.13.0)
  - Locking phpunit/php-code-coverage (9.2.6)
  - Locking phpunit/php-file-iterator (3.0.5)
  - Locking phpunit/php-invoker (3.1.1)
  - Locking phpunit/php-text-template (2.0.4)
  - Locking phpunit/php-timer (5.0.3)
  - Locking phpunit/phpunit (9.5.4)
  - Locking psr/container (1.1.1)
  - Locking psr/event-dispatcher (1.0.0)
  - Locking psr/http-client (1.0.1)
  - Locking psr/http-message (1.0.1)
  - Locking psr/log (1.1.4)
  - Locking psr/simple-cache (1.0.1)
  - Locking psy/psysh (v0.10.8)
  - Locking ralouphie/getallheaders (3.0.3)
  - Locking ramsey/collection (1.1.3)
  - Locking ramsey/uuid (4.1.1)
  - Locking sebastian/cli-parser (1.0.1)
  - Locking sebastian/code-unit (1.0.8)
  - Locking sebastian/code-unit-reverse-lookup (2.0.3)
  - Locking sebastian/comparator (4.0.6)
  - Locking sebastian/complexity (2.0.2)
  - Locking sebastian/diff (4.0.4)
  - Locking sebastian/environment (5.1.3)
  - Locking sebastian/exporter (4.0.3)
  - Locking sebastian/global-state (5.0.2)
  - Locking sebastian/lines-of-code (1.0.3)
  - Locking sebastian/object-enumerator (4.0.4)
  - Locking sebastian/object-reflector (2.0.4)
  - Locking sebastian/recursion-context (4.0.4)
  - Locking sebastian/resource-operations (3.0.3)
  - Locking sebastian/type (2.3.1)
  - Locking sebastian/version (3.0.2)
  - Locking swiftmailer/swiftmailer (v6.2.7)
  - Locking symfony/console (v5.2.8)
  - Locking symfony/css-selector (v5.2.9)
  - Locking symfony/deprecation-contracts (v2.4.0)
  - Locking symfony/error-handler (v5.2.8)
  - Locking symfony/event-dispatcher (v5.2.4)
  - Locking symfony/event-dispatcher-contracts (v2.4.0)
  - Locking symfony/finder (v5.2.9)
  - Locking symfony/http-client-contracts (v2.4.0)
  - Locking symfony/http-foundation (v5.2.8)
  - Locking symfony/http-kernel (v5.2.9)
  - Locking symfony/mime (v5.2.9)
  - Locking symfony/polyfill-ctype (v1.22.1)
  - Locking symfony/polyfill-iconv (v1.22.1)
  - Locking symfony/polyfill-intl-grapheme (v1.22.1)
  - Locking symfony/polyfill-intl-idn (v1.22.1)
  - Locking symfony/polyfill-intl-normalizer (v1.22.1)
  - Locking symfony/polyfill-mbstring (v1.22.1)
  - Locking symfony/polyfill-php72 (v1.22.1)
  - Locking symfony/polyfill-php73 (v1.22.1)
  - Locking symfony/polyfill-php80 (v1.22.1)
  - Locking symfony/process (v5.2.7)
  - Locking symfony/routing (v5.2.9)
  - Locking symfony/service-contracts (v2.4.0)
  - Locking symfony/string (v5.2.8)
  - Locking symfony/translation (v5.2.9)
  - Locking symfony/translation-contracts (v2.4.0)
  - Locking symfony/var-dumper (v5.2.8)
  - Locking theseer/tokenizer (1.2.0)
  - Locking tijsverkoyen/css-to-inline-styles (2.2.3)
  - Locking vlucas/phpdotenv (v5.3.0)
  - Locking voku/portable-ascii (1.5.6)
  - Locking webmozart/assert (1.10.0)
Writing lock file
Installing dependencies from lock file (including require-dev)
Package operations: 104 installs, 0 updates, 0 removals
  - Downloading doctrine/inflector (2.0.3)
  - Downloading webmozart/assert (1.10.0)
  - Downloading dragonmantank/cron-expression (v3.1.0)
  - Downloading symfony/polyfill-mbstring (v1.22.1)
  - Downloading symfony/var-dumper (v5.2.8)
  - Downloading symfony/polyfill-intl-normalizer (v1.22.1)
  - Downloading symfony/polyfill-intl-grapheme (v1.22.1)
  - Downloading symfony/string (v5.2.8)
  - Downloading psr/container (1.1.1)
  - Downloading symfony/service-contracts (v2.4.0)
  - Downloading symfony/console (v5.2.8)
  - Downloading psr/log (1.1.4)
  - Downloading monolog/monolog (2.2.0)
  - Downloading voku/portable-ascii (1.5.6)
  - Downloading graham-campbell/result-type (v1.0.1)
  - Downloading vlucas/phpdotenv (v5.3.0)
  - Downloading symfony/css-selector (v5.2.9)
  - Downloading symfony/deprecation-contracts (v2.4.0)
  - Downloading symfony/routing (v5.2.9)
  - Downloading symfony/process (v5.2.7)
  - Downloading symfony/polyfill-intl-idn (v1.22.1)
  - Downloading symfony/mime (v5.2.9)
  - Downloading symfony/http-foundation (v5.2.8)
  - Downloading symfony/http-client-contracts (v2.4.0)
  - Downloading psr/event-dispatcher (1.0.0)
  - Downloading symfony/event-dispatcher-contracts (v2.4.0)
  - Downloading symfony/event-dispatcher (v5.2.4)
  - Downloading symfony/error-handler (v5.2.8)
  - Downloading symfony/http-kernel (v5.2.9)
  - Downloading symfony/finder (v5.2.9)
  - Downloading symfony/polyfill-iconv (v1.22.1)
  - Downloading swiftmailer/swiftmailer (v6.2.7)
  - Downloading ramsey/collection (1.1.3)
  - Downloading brick/math (0.9.2)
  - Downloading ramsey/uuid (4.1.1)
  - Downloading opis/closure (3.6.2)
  - Downloading symfony/translation-contracts (v2.4.0)
  - Downloading symfony/translation (v5.2.9)
  - Downloading nesbot/carbon (2.48.1)
  - Downloading league/mime-type-detection (1.7.0)
  - Downloading league/commonmark (1.6.2)
  - Downloading laravel/framework (v8.43.0)
  - Downloading filp/whoops (2.12.1)
  - Downloading facade/ignition-contracts (1.0.2)
  - Downloading facade/flare-client-php (1.8.0)
  - Downloading facade/ignition (2.9.0)
  - Downloading fakerphp/faker (v1.14.1)
  - Downloading asm89/stack-cors (v2.0.3)
  - Downloading fruitcake/laravel-cors (v2.0.4)
  - Downloading psr/http-client (1.0.1)
  - Downloading guzzlehttp/psr7 (1.8.2)
  - Downloading guzzlehttp/promises (1.4.1)
  - Downloading guzzlehttp/guzzle (7.3.0)
  - Downloading laravel/sail (v1.7.0)
  - Downloading nikic/php-parser (v4.10.5)
  - Downloading psy/psysh (v0.10.8)
  - Downloading laravel/tinker (v2.6.1)
  - Downloading mockery/mockery (1.4.3)
  - Downloading nunomaduro/collision (v5.4.0)
  - Downloading sebastian/version (3.0.2)
  - Downloading sebastian/type (2.3.1)
  - Downloading sebastian/resource-operations (3.0.3)
  - Downloading sebastian/recursion-context (4.0.4)
  - Downloading sebastian/object-reflector (2.0.4)
  - Downloading sebastian/object-enumerator (4.0.4)
  - Downloading sebastian/global-state (5.0.2)
  - Downloading sebastian/exporter (4.0.3)
  - Downloading sebastian/environment (5.1.3)
  - Downloading sebastian/diff (4.0.4)
  - Downloading sebastian/comparator (4.0.6)
  - Downloading sebastian/code-unit (1.0.8)
  - Downloading sebastian/cli-parser (1.0.1)
  - Downloading phpunit/php-timer (5.0.3)
  - Downloading phpunit/php-text-template (2.0.4)
  - Downloading phpunit/php-invoker (3.1.1)
  - Downloading phpunit/php-file-iterator (3.0.5)
  - Downloading sebastian/lines-of-code (1.0.3)
  - Downloading sebastian/complexity (2.0.2)
  - Downloading sebastian/code-unit-reverse-lookup (2.0.3)
  - Downloading phpunit/php-code-coverage (9.2.6)
  - Downloading phpspec/prophecy (1.13.0)
  - Downloading phar-io/version (3.1.0)
  - Downloading phar-io/manifest (2.0.1)
  - Downloading phpunit/phpunit (9.5.4)
  - Installing doctrine/inflector (2.0.3): Extracting archive
  - Installing doctrine/lexer (1.2.1): Extracting archive
  - Installing symfony/polyfill-ctype (v1.22.1): Extracting archive
  - Installing webmozart/assert (1.10.0): Extracting archive
  - Installing dragonmantank/cron-expression (v3.1.0): Extracting archive
  - Installing symfony/polyfill-php80 (v1.22.1): Extracting archive
  - Installing symfony/polyfill-mbstring (v1.22.1): Extracting archive
  - Installing symfony/var-dumper (v5.2.8): Extracting archive
  - Installing symfony/polyfill-intl-normalizer (v1.22.1): Extracting archive
  - Installing symfony/polyfill-intl-grapheme (v1.22.1): Extracting archive
  - Installing symfony/string (v5.2.8): Extracting archive
  - Installing psr/container (1.1.1): Extracting archive
  - Installing symfony/service-contracts (v2.4.0): Extracting archive
  - Installing symfony/polyfill-php73 (v1.22.1): Extracting archive
  - Installing symfony/console (v5.2.8): Extracting archive
  - Installing psr/log (1.1.4): Extracting archive
  - Installing monolog/monolog (2.2.0): Extracting archive
  - Installing voku/portable-ascii (1.5.6): Extracting archive
  - Installing phpoption/phpoption (1.7.5): Extracting archive
  - Installing graham-campbell/result-type (v1.0.1): Extracting archive
  - Installing vlucas/phpdotenv (v5.3.0): Extracting archive
  - Installing symfony/css-selector (v5.2.9): Extracting archive
  - Installing tijsverkoyen/css-to-inline-styles (2.2.3): Extracting archive
  - Installing symfony/deprecation-contracts (v2.4.0): Extracting archive
  - Installing symfony/routing (v5.2.9): Extracting archive
  - Installing symfony/process (v5.2.7): Extracting archive
  - Installing symfony/polyfill-php72 (v1.22.1): Extracting archive
  - Installing symfony/polyfill-intl-idn (v1.22.1): Extracting archive
  - Installing symfony/mime (v5.2.9): Extracting archive
  - Installing symfony/http-foundation (v5.2.8): Extracting archive
  - Installing symfony/http-client-contracts (v2.4.0): Extracting archive
  - Installing psr/event-dispatcher (1.0.0): Extracting archive
  - Installing symfony/event-dispatcher-contracts (v2.4.0): Extracting archive
  - Installing symfony/event-dispatcher (v5.2.4): Extracting archive
  - Installing symfony/error-handler (v5.2.8): Extracting archive
  - Installing symfony/http-kernel (v5.2.9): Extracting archive
  - Installing symfony/finder (v5.2.9): Extracting archive
  - Installing symfony/polyfill-iconv (v1.22.1): Extracting archive
  - Installing egulias/email-validator (2.1.25): Extracting archive
  - Installing swiftmailer/swiftmailer (v6.2.7): Extracting archive
  - Installing ramsey/collection (1.1.3): Extracting archive
  - Installing brick/math (0.9.2): Extracting archive
  - Installing ramsey/uuid (4.1.1): Extracting archive
  - Installing psr/simple-cache (1.0.1): Extracting archive
  - Installing opis/closure (3.6.2): Extracting archive
  - Installing symfony/translation-contracts (v2.4.0): Extracting archive
  - Installing symfony/translation (v5.2.9): Extracting archive
  - Installing nesbot/carbon (2.48.1): Extracting archive
  - Installing league/mime-type-detection (1.7.0): Extracting archive
  - Installing league/flysystem (1.1.3): Extracting archive
  - Installing league/commonmark (1.6.2): Extracting archive
  - Installing laravel/framework (v8.43.0): Extracting archive
  - Installing filp/whoops (2.12.1): Extracting archive
  - Installing facade/ignition-contracts (1.0.2): Extracting archive
  - Installing facade/flare-client-php (1.8.0): Extracting archive
  - Installing facade/ignition (2.9.0): Extracting archive
  - Installing fakerphp/faker (v1.14.1): Extracting archive
  - Installing fideloper/proxy (4.4.1): Extracting archive
  - Installing asm89/stack-cors (v2.0.3): Extracting archive
  - Installing fruitcake/laravel-cors (v2.0.4): Extracting archive
  - Installing psr/http-message (1.0.1): Extracting archive
  - Installing psr/http-client (1.0.1): Extracting archive
  - Installing ralouphie/getallheaders (3.0.3): Extracting archive
  - Installing guzzlehttp/psr7 (1.8.2): Extracting archive
  - Installing guzzlehttp/promises (1.4.1): Extracting archive
  - Installing guzzlehttp/guzzle (7.3.0): Extracting archive
  - Installing laravel/sail (v1.7.0): Extracting archive
  - Installing nikic/php-parser (v4.10.5): Extracting archive
  - Installing psy/psysh (v0.10.8): Extracting archive
  - Installing laravel/tinker (v2.6.1): Extracting archive
  - Installing hamcrest/hamcrest-php (v2.0.1): Extracting archive
  - Installing mockery/mockery (1.4.3): Extracting archive
  - Installing nunomaduro/collision (v5.4.0): Extracting archive
  - Installing phpdocumentor/reflection-common (2.2.0): Extracting archive
  - Installing phpdocumentor/type-resolver (1.4.0): Extracting archive
  - Installing phpdocumentor/reflection-docblock (5.2.2): Extracting archive
  - Installing sebastian/version (3.0.2): Extracting archive
  - Installing sebastian/type (2.3.1): Extracting archive
  - Installing sebastian/resource-operations (3.0.3): Extracting archive
  - Installing sebastian/recursion-context (4.0.4): Extracting archive
  - Installing sebastian/object-reflector (2.0.4): Extracting archive
  - Installing sebastian/object-enumerator (4.0.4): Extracting archive
  - Installing sebastian/global-state (5.0.2): Extracting archive
  - Installing sebastian/exporter (4.0.3): Extracting archive
  - Installing sebastian/environment (5.1.3): Extracting archive
  - Installing sebastian/diff (4.0.4): Extracting archive
  - Installing sebastian/comparator (4.0.6): Extracting archive
  - Installing sebastian/code-unit (1.0.8): Extracting archive
  - Installing sebastian/cli-parser (1.0.1): Extracting archive
  - Installing phpunit/php-timer (5.0.3): Extracting archive
  - Installing phpunit/php-text-template (2.0.4): Extracting archive
  - Installing phpunit/php-invoker (3.1.1): Extracting archive
  - Installing phpunit/php-file-iterator (3.0.5): Extracting archive
  - Installing theseer/tokenizer (1.2.0): Extracting archive
  - Installing sebastian/lines-of-code (1.0.3): Extracting archive
  - Installing sebastian/complexity (2.0.2): Extracting archive
  - Installing sebastian/code-unit-reverse-lookup (2.0.3): Extracting archive
  - Installing phpunit/php-code-coverage (9.2.6): Extracting archive
  - Installing doctrine/instantiator (1.4.0): Extracting archive
  - Installing phpspec/prophecy (1.13.0): Extracting archive
  - Installing phar-io/version (3.1.0): Extracting archive
  - Installing phar-io/manifest (2.0.1): Extracting archive
  - Installing myclabs/deep-copy (1.10.2): Extracting archive
  - Installing phpunit/phpunit (9.5.4): Extracting archive
62 package suggestions were added by new dependencies, use `composer suggest` to see details.
Generating optimized autoload files
> Illuminate\Foundation\ComposerScripts::postAutoloadDump
> @php artisan package:discover --ansi
Discovered Package: facade/ignition
Discovered Package: fideloper/proxy
Discovered Package: fruitcake/laravel-cors
Discovered Package: laravel/sail
Discovered Package: laravel/tinker
Discovered Package: nesbot/carbon
Discovered Package: nunomaduro/collision
Package manifest generated successfully.
74 packages you are using are looking for funding.
Use the `composer fund` command to find out more!
> @php artisan key:generate --ansi
Application key set successfully.
➜  PABWEB-LARAVEL
```
Hasil dari paket unduhan akan membuat struktur direktorinya seperti berikut:

![direktori](assets/img/Screen%20Shot%202021-05-27%20at%202.19.24%20PM.png)



## Langkah 2 - Menjalankan Project Laravel

Setelah proses installasi selesai, kita bisa mencoba menjalankan project Laravel-nya. Silahkan jalankan perintah di bawah ini :

```Apache
cd 21-pabweb
```
Perintah `cd` di atas digunakan untuk masuk ke dalam folder project Laravel

![cd](assets/img/Screen%20Shot%202021-05-27%20at%202.24.03%20PM.png)

_Untuk lebih mudah silahkan gunakan vscode_

Selanjutnya ketikan perintah berikut

```Apache
php artisan serve
```
![serve](assets/img/Screen%20Shot%202021-05-27%20at%202.31.20%20PM.png)

Jika berhasil maka project kita akan dijalankan menggunakan port `8000` di dalam localhost, kita bisa membuka di http://localhost:8000 dan jika berhasil kurang lebih tampilannya seperti berikut ini :

![8000](assets/img/Screen%20Shot%202021-05-27%20at%202.29.34%20PM.png)

## Langkah 3 - Menjalankan Storage Link

Silahkan jalankan perintah di bawah ini untuk membuat `symlink folder storage agar bisa di akses melalui folder public Laravel.`

```Apache
php artisan storage:link
```
![link](assets/img/Screen%20Shot%202021-05-27%20at%202.36.42%20PM.png)

Di praktikum selanjutnya kita akan belajar bagaimana cara membuat `migration` dan menjalankan `migration` di dalam `Laravel 8`.

