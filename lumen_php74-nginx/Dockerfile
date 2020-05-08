FROM php:7.4-fpm

RUN apt update && apt install -y \
        supervisor \
        nginx \
        libcurl4-openssl-dev \
        libpq-dev \
        libonig-dev \
        libmcrypt-dev \
        zlib1g-dev \
        libmemcached-dev \
        libzip-dev \
      && pecl install \
        mcrypt \
        igbinary \
        memcached \
        redis \
      && docker-php-ext-install \
        curl \
        pdo \
        pdo_pgsql \
        pdo_mysql \
        mbstring \
        mysqli \
        zip \
      && docker-php-ext-enable \
        mcrypt \
        igbinary \
        memcached \
        opcache \
        redis

COPY conf/nginx.conf /etc/nginx/sites-enabled/default
COPY conf/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

EXPOSE 80

CMD ["/usr/bin/supervisord", "-n", "-c", "/etc/supervisor/conf.d/supervisord.conf"]
