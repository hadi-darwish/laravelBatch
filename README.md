# Laravel BATCH (BULK)

Insert and update batch (bulk) in laravel

[![License](https://poser.pugx.org/hadi-darwish/laravel-batch/license)](https://packagist.org/packages/hadi-darwish/laravel-batch)
[![Latest Stable Version](https://poser.pugx.org/hadi-darwish/laravel-batch/v/stable)](https://packagist.org/packages/hadi-darwish/laravel-batch)
[![Total Downloads](https://poser.pugx.org/hadi-darwish/laravel-batch/downloads)](https://packagist.org/packages/hadi-darwish/laravel-batch)
[![Daily Downloads](https://poser.pugx.org/hadi-darwish/laravel-batch/d/daily)](https://packagist.org/packages/hadi-darwish/laravel-batch)

# Install

`composer require hadi-darwish/laravel-batch`

# Service Provider

file app.php in array providers :

`Hadi\Batch\BatchServiceProvider::class,`

# Aliases

file app.php in array aliases :

`'Batch' => Hadi\Batch\BatchFacade::class,`

# Example Update 1

```php
use App\Models\User;

$userInstance = new User;
$value = [
     [
         'id' => 1,
         'status' => 'active',
         'nickname' => 'Mohammad'
     ] ,
     [
         'id' => 5,
         'status' => 'deactive',
         'nickname' => 'Ghanbari'
     ] ,
];
$index = 'id';

Batch::update($userInstance, $value, $index);
```

# Example Update 2

```php
use App\Models\User;

$userInstance = new User;
$value = [
     [
         'id' => 1,
         'status' => 'active'
     ],
     [
         'id' => 5,
         'status' => 'deactive',
         'nickname' => 'Ghanbari'
     ],
     [
         'id' => 10,
         'status' => 'active',
         'date' => Carbon::now()
     ],
     [
         'id' => 11,
         'username' => 'hadi-darwish'
     ]
];
$index = 'id';

Batch::update($userInstance, $value, $index);
```

# Example Increment / Decrement

```php
use App\Models\User;

$userInstance = new User;
$value = [
     [
         'id' => 1,
         'balance' => ['+', 500] // Add
     ] ,
     [
         'id' => 2,
         'balance' => ['-', 200] // Subtract
     ] ,
     [
         'id' => 3,
         'balance' => ['*', 5] // Multiply
     ] ,
     [
         'id' => 4,
         'balance' => ['/', 2] // Divide
     ] ,
     [
         'id' => 5,
         'balance' => ['%', 2] // Modulo
     ] ,
];
$index = 'id';

Batch::update($userInstance, $value, $index);
```

# Example Insert

```php
use App\Models\User;

$userInstance = new User;
$columns = [
     'firstName',
     'lastName',
     'email',
     'isActive',
     'status',
];
$values = [
     [
         'Mohammad',
         'Ghanbari',
         'emailSample_1@gmail.com',
         '1',
         '0',
     ] ,
     [
         'Saeed',
         'Mohammadi',
         'emailSample_2@gmail.com',
         '1',
         '0',
     ] ,
     [
         'Avin',
         'Ghanbari',
         'emailSample_3@gmail.com',
         '1',
         '0',
     ] ,
];
$batchSize = 500; // insert 500 (default), 100 minimum rows in one query

$result = Batch::insert($userInstance, $columns, $values, $batchSize);
```

```php
// result : false or array

sample array result:
Array
(
    [totalRows]  => 384
    [totalBatch] => 500
    [totalQuery] => 1
)
```

# Example called from model

Add `HasBatch` trait into model:

```php
namespace App\Models;

use Hadi\Batch\Traits\HasBatch;

class User extends Model
{
    use HasBatch;
}
```

And call `batchUpdate()` or `batchInsert()` from model:

```php
use App\Models\User;

// ex: update
User::batchUpdate($value, $index);

// ex: insert
User::batchInsert($columns, $values, $batchSize);
```

# Helper batch()

```php
// ex: update

$result = batch()->update($userInstance, $value, $index);


// ex: insert

$result = batch()->insert($userInstance, $columns, $values, $batchSize);
```

# Tests

If you don't have phpunit installed on your project, first run `composer require phpunit/phpunit`

In the root of your laravel app, run `./vendor/bin/phpunit ./vendor/hadi-darwish/laravel-batch/tests`

# Donate

BTC Address: 14XQEuVKuZp8q59h3Jk9Q2wi45368aEbyG

DOGE Address: DMsFurgSP2LTny8wkco3cE3ZhgQrFAJLp8
