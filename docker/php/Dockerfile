FROM php:5.6-apache

RUN apt-get update && apt-get install -y ssl-cert \
  --no-install-recommends && rm -r /var/lib/apt/lists/*

ADD conf.d/vhost.conf /etc/apache2/sites-enabled/000-default.conf
ADD conf.d/ssl-default.conf /etc/apache2/sites-enabled/ssl-default.conf
ADD conf.d/php.ini /usr/local/etc/php/php.ini

RUN a2enmod rewrite

RUN a2enmod ssl

EXPOSE 443

RUN usermod -u 1000 www-data