[![Latest Stable Version](https://poser.pugx.org/hrace009/laravel6settings/v/stable)](https://packagist.org/packages/hrace009/laravel6settings)
[![Total Downloads](https://poser.pugx.org/hrace009/laravel6settings/downloads)](https://packagist.org/packages/hrace009/laravel6settings)
[![Latest Unstable Version](https://poser.pugx.org/hrace009/laravel6settings/v/unstable)](https://packagist.org/packages/hrace009/laravel6settings)
[![License](https://poser.pugx.org/hrace009/laravel6settings/license)](https://packagist.org/packages/hrace009/laravel6settings)

# Laravel6Settings
Laravel 6.x Persistent Settings (Database + Cache)  

Re-Publish new migration file

    $ php artisan vendor:publish --provider="hrace009\Laravel6Settings\SettingsServiceProvider" --force
    
And run

    $ php artisan migrate

## How to Install
Require this package with composer ([Packagist](https://packagist.org/packages/hrace009/laravel6settings)) using the following command:

    composer require hrace009/laravel6settings

or modify your `composer.json`:
   
       "require": {
          "hrace009/laravel6settings": "1.*"
       }
       
then run `composer update`:

After updating composer, Register the ServiceProvider to the `providers` array in `config/app.php`

    'hrace009\Laravel6Settings\SettingsServiceProvider',
    
Add an alias for the facade to `aliases` array in  your `config/app.php`

    'Settings'  => hrace009\Laravel6Settings\Facades\Settings::class,

Publish the config and migration files now (Attention: This command will not work if you don't follow previous instruction):

    $ php artisan vendor:publish --provider="hrace009\Laravel6Settings\SettingsServiceProvider" --force
    
Change `config/settings.php` according to your needs. If you change `db_table`, don't forget to change the table's name
in the migration file as well.
    
Create the `settings` table. 

    $ php artisan migrate
    

## How to Use it?

Set a value

    Settings::set('key', 'value');
    
Get a value

    $value = Settings::get('key');
    
Get a value with Default Value.

    $value = Settings::get('key', 'Default Value');
    
> Note: If key is not found (null) in cache or settings table, it will return default value

Get a value via an helper
    
    $value = settings('key');
    $value = settings('key', 'default value');
    
Forget a value

    Settings::forget('key');

Forget all values

    Settings::flush();
    
## Fallback to Laravel Config

How to activate?

    // Change your config/settings.php
    'fallback'   => true
    
Example

    /* 
     * If the value with key => mail.host is not found in cache or DB of Larave Settings
     * it will return same value as config::get('mail.host');
     */     
    Settings::get('mail.host');

> Note: It will work if default value in laravel setting is not set
    
### Changelogs
v1.0 - Jan 13th, 2020

* New release

### License

The Laravel 6 Persistent Settings is open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT)

