FROM php:fpm-alpine

WORKDIR /var/www

RUN apk add -Uuv --no-cache --virtual build-deps \
    gcc \
    g++ \
    dpkg \
    make \
    php7-dev \
    libtool \
    autoconf \
    pcre-dev \
    cyrus-sasl-dev \
    && apk add --no-cache icu \
    icu-dev \ 
    git \
    bash \
    mc \
    wget \
    freetype-dev \
    imagemagick-dev \
    imagemagick \
    libintl \
    libzip-dev \
    libjpeg-turbo-dev \
    libpng-dev \
    libwebp-dev \
    postgresql-dev \
    supervisor \
    zlib-dev \
    shadow \
    $PHPIZE_DEPS \
    libmemcached-dev \
    && pecl install memcached \
    && docker-php-ext-enable memcached \
    # Clean up
    && apk del build-deps \
    && rm -fr /tmp/pear \
    && rm -rf /tmp/* /var/cache/apk/* \
    \
    # Install imagick
    && pecl install imagick-3.4.4 \
    && docker-php-ext-enable imagick \
    \
    # Clean up
    && docker-php-source delete \
    \
    #xdebug
    && pecl install xdebug-2.9.6 \
    && docker-php-ext-enable xdebug \
    \
    # composer
    && wget https://getcomposer.org/installer -O - -q \
    | php -- --install-dir=/bin --filename=composer --quiet \
    \
    # php extensions
    && docker-php-ext-install -j4 intl pdo pdo_mysql pdo_pgsql mysqli  pcntl gd bcmath posix zip opcache sockets calendar exif && \
    docker-php-ext-configure opcache && \
    docker-php-ext-configure pdo_pgsql && \
    docker-php-ext-configure pdo_mysql && \
    docker-php-ext-configure mysqli && \
    docker-php-ext-configure bcmath && \
    docker-php-ext-configure exif && \
    docker-php-ext-configure gd \
    \
    && usermod -u 1000 www-data && groupmod -g 1000 www-data \
