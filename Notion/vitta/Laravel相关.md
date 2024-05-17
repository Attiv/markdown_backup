- You made a reference to a non-existent script @php artisan package:discover
- 1071 Specified key was too long; max key length is 767 bytes
- created_at 改为 int 时间戳
- env null
- laravel 500 错误没有错误信息
- 使用 socket连接mysql

# You made a reference to a non-existent script @php artisan package:discover

可以使用 `composer global update`  
或  
`composer global self-update`

# 1071 Specified key was too long; max key length is 767 bytes

在 `AppServiceProvider.php`:

```Plain
public function boot()
    {
        Schema::defaultStringLength(191);
    }
```

# created_at 改为 int 时间戳

在 `model`中:

```Plain
public function fromDateTime($value)
    {
        return strtotime(parent::fromDateTime($value));
    }
```

# `env` null

`php artisan config:clear`

# laravel 500 错误没有错误信息

可以在 `index.php`  
加上  
`ini_set('display_errors', 'On');`

# 使用 socket连接mysql

在 `.env`文件里:

```Plain
DB_SOCKET=/Applications/MAMP/tmp/mysql/mysql.sock
```

  

[toc]

# You made a reference to a non-existent script @php artisan package:discover

可以使用 `composer global update`  
或  
`composer global self-update`

# 1071 Specified key was too long; max key length is 767 bytes

在 `AppServiceProvider.php`:

```Plain
    public function boot()
    {
        Schema::defaultStringLength(191);
    }
```

# created_at 改为 int 时间戳

在 `model`中:

```Plain
    public function fromDateTime($value)
    {
        return strtotime(parent::fromDateTime($value));
    }
```

# `env` null

`php artisan config:clear`

# laravel 500 错误没有错误信息

可以在 `index.php`  
加上  
`ini_set('display_errors', 'On');`

# 使用 socket连接mysql

在 `.env`文件里:

```Plain
DB_SOCKET=/Applications/MAMP/tmp/mysql/mysql.sock
```