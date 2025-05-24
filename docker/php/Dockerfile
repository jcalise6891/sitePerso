FROM php:8.3-fpm

# Pré-requis
RUN apt-get update && apt-get install -y \
    git curl zip unzip libpng-dev libonig-dev libxml2-dev libzip-dev \
    libpq-dev libcurl4-openssl-dev libssl-dev \
    && docker-php-ext-install pdo_mysql mbstring zip exif pcntl bcmath

# Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Node.js + npm (Vite, Mix, etc.)
RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash - \
    && apt-get install -y nodejs \
    && npm install -g npm

# Dossier de travail
WORKDIR /var/www/html