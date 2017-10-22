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
