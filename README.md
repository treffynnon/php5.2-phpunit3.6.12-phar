# phpunit for PHP 5.2

Generate a phar file from phpunit 3.6.12 (the last version to support
PHP 5.2).

## Grab it

You can get a compiled phar from the [releases page](https://github.com/treffynnon/php5.2-phpunit3.6.12-phar/releases).

## Installation

Clone this repo down and run

    composer install

## Build the phar

    composer run-script build

You'll now have phpunit-php52.phar in the directory

## Run it against your tests

    ./phpunit-php52.phar -c path/to/phpunit.xml
