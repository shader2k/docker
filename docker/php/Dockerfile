FROM php:7.3-fpm

ARG CURRENT_USER

RUN usermod -u ${CURRENT_USER? invalid argument} www-data
RUN groupmod -g ${CURRENT_USER? invalid argument} www-data

# Install dependencies
RUN apt-get update && apt-get install -y \
    openssl \
    sqlite3 \
    zip \
    unzip \
    zlib1g-dev \
    libzip-dev \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    git \
    curl

# Clear cache
RUN rm -rf /var/lib/apt/lists/*

RUN apt-get update -yqq && \
    apt-get install -y apt-utils && \
    pecl channel-update pecl.php.net

RUN apt-get update && apt-get install -y wget git unzip \
    && pecl install xdebug-2.9.0 \
    && docker-php-ext-enable xdebug

# Install extensions
RUN docker-php-ext-install mysqli pdo pdo_mysql zip mbstring tokenizer bcmath
RUN docker-php-ext-configure gd --with-gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ --with-png-dir=/usr/include/
RUN docker-php-ext-install gd

# Copy configuration
COPY ./config/php.ini /usr/local/etc/php/php.ini
COPY ./config/opcache.ini /usr/local/etc/php/conf.d/opcache.ini

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer


# Clean
RUN apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /var/cache/*

RUN apt-get update && apt-get install sudo -y

USER www-data
