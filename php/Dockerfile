ARG PHP_VERSION=8.2
FROM php:${PHP_VERSION}-fpm

# System deps for PHP extensions
RUN apt-get update && apt-get install -y --no-install-recommends \
    libicu-dev \
    libzip-dev \
    libjpeg-dev libpng-dev libfreetype6-dev \
    libxml2-dev \
    libpq-dev \
    libsodium-dev \
    zlib1g-dev \
    unzip git curl \
    && rm -rf /var/lib/apt/lists/*

# Configure GD with JPEG & Freetype
RUN docker-php-ext-configure gd --with-freetype --with-jpeg

# Build PHP extensions
RUN docker-php-ext-install -j$(nproc) \
    intl \
    gd \
    opcache \
    zip \
    xml \
    soap \
    pgsql pdo_pgsql \
    exif \
    sodium

# Reasonable OPcache defaults (development-friendly)
RUN { \
      echo 'opcache.enable=1'; \
      echo 'opcache.memory_consumption=128'; \
      echo 'opcache.max_accelerated_files=10000'; \
      echo 'opcache.revalidate_freq=2'; \
      echo 'opcache.validate_timestamps=1'; \
    } > /usr/local/etc/php/conf.d/opcache.ini

# File upload limits/tweaks
RUN { \
      echo 'memory_limit=512M'; \
      echo 'upload_max_filesize=200M'; \
      echo 'post_max_size=200M'; \
      echo 'max_execution_time=300'; \
    } > /usr/local/etc/php/conf.d/uploads.ini

# Create moodledata with safe perms
RUN mkdir -p /var/www/moodledata && chown -R www-data:www-data /var/www/moodledata

WORKDIR /var/www/moodle
