FROM php:7.0-apache
LABEL maintainer="Stefano Martins <xstefanox AT gmail DOT com>"

RUN apt-get update -qq && \
    apt-get install -y \
    libcurl4-gnutls-dev \
    librtmp-dev \
    libpng-dev \
    firebird-dev \
    libmcrypt-dev \
    libreadline-dev \
    libxml2-dev \
    memcached

RUN docker-php-ext-install -j$(nproc) curl 
RUN docker-php-ext-install -j$(nproc) gd 
RUN docker-php-ext-install -j$(nproc) interbase 
RUN docker-php-ext-install -j$(nproc) mbstring 
RUN docker-php-ext-install -j$(nproc) mcrypt 
RUN docker-php-ext-install -j$(nproc) mysqli 
RUN docker-php-ext-install -j$(nproc) pdo_mysql 
RUN docker-php-ext-install -j$(nproc) xml 
RUN docker-php-ext-install -j$(nproc) simplexml

#  Altera configurações do PHP
COPY uploads.ini /usr/local/etc/php/conf.d/uploads.ini
COPY default_charset.ini /usr/local/etc/php/conf.d/default_charset.ini

# Habilita módulos do Apache
RUN a2enmod rewrite headers

COPY charset.conf /etc/apache2/conf-available/charset.conf
COPY 000-default.conf /etc/apache2/sites-available/000-default.conf

