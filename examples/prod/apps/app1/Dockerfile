FROM php:8.4-fpm

RUN apt-get update && apt-get install -y \
    git \
    unzip \
    zip \
    curl \
    libzip-dev \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    libicu-dev \
    libonig-dev \
    libxml2-dev

RUN docker-php-ext-configure gd \
    --with-freetype \
    --with-jpeg

RUN docker-php-ext-install \
    pdo_mysql \
    mysqli \
    bcmath \
    exif \
    intl \
    gd \
    zip \
    opcache

RUN pecl install redis \
    && docker-php-ext-enable redis

COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

WORKDIR /var/www

CMD ["php-fpm"]

