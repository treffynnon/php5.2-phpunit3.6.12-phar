# phpunit for PHP 5.2

Generate a phar file from phpunit 3.6.12 (the last version to support
PHP 5.2).

## Why?

A PHP project I maintain ([idiorm](github.com/j4mie/idiorm)) maintains PHP 5.2 support and I wanted to ensure
this wasn't broken by having Travis CI run the tests. Unfortunately, there was no easy
way to run the tests as PHPUnit hasn't released a PHP 5.2 compatible release as a phar
file and composer isn't supported on PHP 5.2 either.

PHPUnit used to be installed via PEAR prior to version 3.7, but the team stopped that
PEAR server years ago so there wasn't a simple way to get PHPUnit 3.6.17 on PHP 5.2.

I also wanted to be able to run the tests locally on PHP 5.2 easily too.

## Grab it

You can get a compiled phar from the [releases page](https://github.com/treffynnon/php5.2-phpunit3.6.12-phar/releases).

## Building

Clone this repo down and run

    composer install
    composer run-script build

You'll now have phpunit-php52.phar in the project directory.

If you get a warning from Box about phar.readonly you re-run the command with

    php -d phar.readonly=off composer run-script build

or you can disable it permanently you php.ini file.

## Using it

### Locally on your project tests

    ./phpunit-php52.phar -c path/to/phpunit.xml

### Using it on Travis CI

Here is a barebones `.travis.yml` file to make use of this project to run tests on PHP 5.2.

```yaml
language: php
matrix:
  include:
    - php: 5.2
      dist: precise
before_install: pecl install phar
install: |
  export X="$HOME/.build-deps/bin"
  mkdir -p "$X"
  curl -sSfL https://github.com/treffynnon/php5.2-phpunit3.6.12-phar/releases/download/1.0.0/php52-phpunit.phar -o "$X/phpunit"
  chmod +x "$X/phpunit"
script: $X/phpunit --colors --coverage-text
```

For a more involved configuration (including other versions of PHP etc) please see
the one I wrote for Idiorm: https://github.com/j4mie/idiorm/blob/master/.travis.yml

Note that it uses an environment var to ensure it only does all the extra work on PHP 5.2
and not the other PHP versions.