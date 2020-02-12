FROM php:5.6-apache

RUN apt-get update \
    && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev

# enable rewrite.
RUN cd /etc/apache2/mods-enabled \
    && ln -s ../mods-available/rewrite.load

# install composer
COPY --from=composer:1.8.6 /usr/bin/composer /usr/bin/composer

# install xdebug
RUN pecl install xdebug-2.5.5 && docker-php-ext-enable xdebug

# update httpd.conf
COPY ./sites-available/000-default.conf /etc/apache2/sites-available/000-default.conf

# update php.ini
COPY ./php.ini /usr/local/etc/php/php.ini

WORKDIR /var/www/html
