FROM php:5.6-apache
MAINTAINER tuki0918@gmail.com

RUN apt-get update && apt-get install -y ssl-cert \
  --no-install-recommends && rm -r /var/lib/apt/lists/*

RUN apt-get update && apt-get install -y git zlib1g-dev \
  --no-install-recommends && rm -r /var/lib/apt/lists/* \
  && docker-php-ext-install zip

RUN docker-php-ext-install pdo_mysql mysqli mbstring

RUN pecl install xdebug
RUN docker-php-ext-enable xdebug

ADD conf.d/vhost.conf /etc/apache2/sites-enabled/000-default.conf
ADD conf.d/ssl-default.conf /etc/apache2/sites-enabled/ssl-default.conf
ADD conf.d/php.ini /usr/local/etc/php/php.ini
ADD conf.d/xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

RUN a2enmod rewrite
RUN a2enmod ssl

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \
    composer config -g github-oauth.github.com bb2e1fcd213e3b67f16f47c5bc72848bc1c7042d && \
    composer global require phpunit/phpunit

ENV HOME /root
ENV PATH $HOME/.composer/vendor/bin:$PATH

EXPOSE 80
EXPOSE 443

RUN usermod -u 1000 www-data