# Forked from [cristianorsolin/docker-php-5.3-apache](https://github.com/cristianorsolin/docker-php-5.3-apache)
 Modified to use mysqlnd for pdo driver, !Warning i have discarded the SSL verifier when building, dont use this version for production, use the original.
 


# PHP 5.3 Apache

PHP 5.3 [reached EOL](http://php.net/eol.php) on 14 Aug 2014 and thus, official docker support was [dropped](https://github.com/docker-library/php/pull/20). I still needed to run 5.3 so I built this image based on the latest official builds of PHP.

# What is PHP?

PHP is a server-side scripting language designed for web development, but which can also be used as a general-purpose programming language. PHP can be added to straight HTML or it can be used with a variety of templating engines and web frameworks. PHP code is usually processed by an interpreter, which is either implemented as a native module on the web-server or as a common gateway interface (CGI).

> [wikipedia.org/wiki/PHP](http://en.wikipedia.org/wiki/PHP)

![logo](https://raw.githubusercontent.com/docker-library/docs/master/php/logo.png)

# How to use this image.

## With Command Line

For PHP projects run through the command line interface (CLI), you can do the following.

### Create a `Dockerfile` in your PHP project

    FROM jinraynor1/php5.3
    COPY . /usr/src/myapp
    WORKDIR /usr/src/myapp
    CMD [ "php", "./your-script.php" ]

Then, run the commands to build and run the Docker image:

    docker build -t my-php-app .
    docker run -it --rm --name my-running-app my-php-app

### Run a single PHP script

For many simple, single file projects, you may find it inconvenient to write a complete `Dockerfile`. In such cases, you can run a PHP script by using the PHP Docker image directly:

    docker run -it --rm --name my-running-script -v "$PWD":/usr/src/myapp -w /usr/src/myapp jinraynor1/php5.3 php your-script.php

### Installing modules

To install additional modules use a `Dockerfile` like this:

``` Dockerfile
FROM jinraynor1/php5.3

# Installs curl
RUN docker-php-ext-install curl
```

Then build the image:

``` bash
$ docker build -t my-php .
```

### Without a `Dockerfile`

If you don't want to include a `Dockerfile` in your project, it is sufficient to do the following:

    docker run -it --rm --name my-php-app -v "$PWD":/var/www/html jinraynor1/php5.3

## Credits

A big credit to [helderco](https://github.com/helderco/docker-php-5.3) for the `fpm` version
of this image.

# License

View [license information](http://php.net/license/) for the software contained in this image.
