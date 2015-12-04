FROM php:5.6-apache
MAINTAINER tuki0918@gmail.com

RUN apt-get update && apt-get install -y ssl-cert \
  --no-install-recommends && rm -r /var/lib/apt/lists/*

RUN docker-php-ext-install pdo_mysql mysqli mbstring

RUN pecl install xdebug
RUN docker-php-ext-enable xdebug

ADD conf.d/vhost.conf /etc/apache2/sites-enabled/000-default.conf
ADD conf.d/ssl-default.conf /etc/apache2/sites-enabled/ssl-default.conf
ADD conf.d/php.ini /usr/local/etc/php/php.ini
ADD conf.d/xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

RUN a2enmod rewrite
RUN a2enmod ssl

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

EXPOSE 80
EXPOSE 443

RUN usermod -u 1000 www-data