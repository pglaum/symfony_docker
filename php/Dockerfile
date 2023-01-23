FROM php:8.2 AS base

RUN apt-get update && apt-get install -y git wget
RUN wget https://get.symfony.com/cli/installer -O - | bash
RUN ls -a
RUN mv ~/.symfony5/bin/symfony /usr/local/bin/symfony
RUN chmod +x /usr/local/bin/symfony

# 1. Install development packages and clean up apt cache.
RUN apt-get update && apt-get install -y \
    build-essential \
    curl \
    g++ \
    git \
    libbz2-dev \
    libfreetype6-dev \
    libicu-dev \
    libjpeg62-turbo-dev \
    libjpeg-dev \
    libmcrypt-dev \
    libpng-dev \
    libreadline-dev \
    sudo \
    unzip \
    zip \
    libzip-dev \
    libxslt1-dev \
 && rm -rf /var/lib/apt/lists/*

# 4. Start with base PHP config, then add extensions.
RUN mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"

RUN docker-php-ext-configure gd --enable-gd --with-freetype --with-jpeg
RUN docker-php-ext-install \
    bcmath \
    bz2 \
    calendar \
    iconv \
    intl \
    opcache \
    pdo_mysql \
    mysqli \
    gd \
    zip \
    xsl

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php --filename=composer --install-dir=/usr/local/bin
RUN mkdir /.composer
RUN chmod -Rf 777 /.composer
