FROM php:5.6-fpm

WORKDIR /var/www

RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libicu-dev \
    libmcrypt-dev \
    libxslt1-dev \
    libpq-dev \
    libzip-dev \
    zlib1g-dev \
    libmemcached11 \
    libmemcachedutil2 \
    build-essential \
    libmemcached-dev \
    libxml2 \
    libxml2-dev \
    zip \
    unzip \
    git \
    wget \
    procps \
    vim \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd \
    # && docker-php-ext-install -j$(nproc) libxml \
    && docker-php-ext-install -j$(nproc) mcrypt \ 
    && docker-php-ext-install -j$(nproc) mysql \
    && docker-php-ext-install -j$(nproc) mysqli \
    && docker-php-ext-install -j$(nproc) pcntl \
    # && docker-php-ext-install -j$(nproc) pcre \
    && docker-php-ext-install -j$(nproc) pdo_mysql \
    && docker-php-ext-install -j$(nproc) sockets \
    && docker-php-ext-install -j$(nproc) zip \
    && docker-php-ext-install -j$(nproc) pcntl


RUN pecl install memcached-2.2.0 \
    pecl install redis-2.2.8 \
    && docker-php-ext-enable memcached redis

RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

# # 命令补全
# RUN apt-get install -y bash-completion \
#     echo "if [ -f /etc/bash_completion ]; then \
#     . /etc/bash_completion \
#     fi" >> ~/.bashrc

EXPOSE 9000