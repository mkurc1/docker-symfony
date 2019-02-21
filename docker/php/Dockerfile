FROM php:7.2-fpm-alpine

RUN addgroup -g 1000 www && \
    adduser -D -u 1000 -G www -h /var/www www

RUN apk add --no-cache bash vim git \
    openssl \
    libcurl curl curl-dev \
    autoconf gcc g++ make \
    # Needed for zip extension
    zlib-dev \
    libmemcached-dev \
    openssh

RUN \
    docker-php-ext-install json && \
    docker-php-ext-install ctype && \
    docker-php-ext-install pdo && \
    docker-php-ext-install pdo_mysql && \
    docker-php-ext-install curl && \
    docker-php-ext-install bcmath && \
    docker-php-ext-install mbstring && \
    docker-php-ext-install opcache && \
    docker-php-ext-install zip

### composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

### nodejs
RUN apk update && apk add nodejs nodejs-npm yarn

COPY --chown=www:www . /data
USER www
WORKDIR /data

EXPOSE 9000

STOPSIGNAL SIGQUIT

CMD ["php-fpm"]
