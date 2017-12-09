# PHP-Easy-Container  

[![Build Status](https://travis-ci.org/johnroyer/php-easy-container.svg?branch=master)](https://travis-ci.org/johnroyer/php-easy-container)
[![Coverage Status](https://coveralls.io/repos/github/johnroyer/php-easy-container/badge.svg)](https://coveralls.io/github/johnroyer/php-easy-container)

An implement for singleton and some features.


## Requirement

- PHP >= 5.6


## Simple Usage

Put whatever you want into container:

```php
use \Zeroplex\Container\Container;

$c = new Container;

// set value as singleton
$c['pi'] = 3.14159;
$c['db'] = new PDO(
    'mysql:dbname=mydb;host=localhost',
    'user',
    'password'
);
```

Get things out from container:

```php
$c['pi'];  // 3.14159
$c['db'];  // object(PDO)
```


## Singleton

If you use `ArrayAccess` interfaces to access the data from container, container will treat them as sinleton, as example ablove.

You can also use method `singleton()` to put data into container:

```php
$c->singleton('db') = new PDO(
    'mysql:dbname=mydb;host=localhost',
    'user',
    'password'
);

$c->get('db');  // object(PDO)
```


Sometimes, you are not sure if an DB connection should initialize while program start up. Maybe connect to DB when it is really needed is a better idea.

Use a `Closure` to let container known you want to initialize it later:

```php
$c['db'] = function () {
    return new PDO(
        'mysql:dbname=test;host=localhost',
        'johnroyer',
        'Zer0p!exl,'
    );
};

$c->get('db');  // new PDO if and only if someone get it
                // object(PDO)
```




## Provide

Container can contains things with states, can also contains things stateless. `provide()` method stores bussiness logic or workflow which is stateless.

```php
$c->provide('pi', 3.14159265359);
$c['pi'];  // 3.14159265359

$c->provide('nowDate', function() {
    // always return special format of date
    return (new DateTime())
        ->format('Y-m-d');
});
$c->['nowDate'];  // "2017-12-01"
```
