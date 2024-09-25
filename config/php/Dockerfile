# php-fpm 이미지를 베이스로 사용 (Debian 기반)
FROM php:fpm

# 필수 패키지 업데이트 및 설치
RUN apt-get update && apt-get install -y \
    g++ \
    make \
    autoconf \
    libmcrypt-dev \
    libonig-dev \
    libxml2-dev \
    libicu-dev \
    tzdata \
    --no-install-recommends

# pecl 확장 설치 (redis, xdebug, mcrypt)
RUN pecl install redis \
    && pecl install xdebug \
    && pecl install mcrypt \
    && docker-php-ext-enable redis xdebug mcrypt

# PHP 확장 설치 (mysqli 등)
RUN docker-php-ext-install \
    intl \
    pcntl \
    mysqli \
    sockets \
    mbstring \
    calendar \
    pdo_mysql \
    opcache


# Composer 설치
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer

# php.ini 복사
COPY php.ini /usr/local/etc/php/php.ini

# php-fpm 실행
CMD ["php-fpm"]
