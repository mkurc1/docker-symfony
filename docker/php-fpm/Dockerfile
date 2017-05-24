FROM php:7.0-fpm

MAINTAINER mkurc1 <mkurc1@gmail.com>

# Set timezone
RUN rm /etc/localtime
RUN ln -s /usr/share/zoneinfo/Europe/Warsaw /etc/localtime
RUN "date"

# Install packages
RUN apt-get update && apt-get install -y \
        vim \
        git \
        unzip \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        libicu-dev \
    && docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

RUN docker-php-ext-configure intl
RUN docker-php-ext-install pdo pdo_mysql intl

# Config PHP
RUN echo "mbstring.internal_encoding = UTF-8" >> /usr/local/etc/php/conf.d/docker-php.ini
RUN echo "mbstring.http_input = UTF-8" >> /usr/local/etc/php/conf.d/docker-php.ini
RUN echo "date.timezone = Europe/Warsaw" >> /usr/local/etc/php/conf.d/docker-php.ini
RUN echo "memory_limit = 1G" >> /usr/local/etc/php/conf.d/docker-php.ini

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version

# Add bash alias
RUN echo 'alias sf="php app/console"' >> ~/.bashrc
RUN echo 'alias sfcl="php app/console cache:clear"' >> ~/.bashrc
RUN echo 'alias sf3="php bin/console"' >> ~/.bashrc

WORKDIR /var/www/symfony
