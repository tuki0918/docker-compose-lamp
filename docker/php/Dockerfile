FROM php:5.6-apache

ADD conf.d/vhost.conf /etc/apache2/sites-enabled/000-default.conf
ADD conf.d/php.ini /usr/local/etc/php/php.ini

RUN a2enmod rewrite

RUN usermod -u 1000 www-data