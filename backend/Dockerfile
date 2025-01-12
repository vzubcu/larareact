# Folosește imaginea oficială PHP
FROM php:8.1-fpm

# Instalează extensiile și dependințele necesare
RUN apt-get update && apt-get install -y \
    curl \
    zip \
    unzip \
    git \
    libpq-dev \
    libonig-dev \
    libzip-dev \
    procps \
    && docker-php-ext-install pdo pdo_mysql mbstring zip exif pcntl bcmath

# Instalează Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Setează directorul de lucru
WORKDIR /var/www

# Copiază fișierele Laravel în container
COPY . .

# Instalează dependențele Laravel
RUN composer install --no-scripts --no-autoloader
RUN composer dump-autoload

# Setează permisiunile pentru directoare
RUN chown -R www-data:www-data storage bootstrap/cache
RUN chmod -R 775 storage bootstrap/cache

EXPOSE 9000
CMD ["php-fpm"]
