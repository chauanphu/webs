# Use the official PHP 7.4 Apache base image
FROM php:8.2-apache

# Set the working directory to /var/www/html
WORKDIR /var/www/html

# Install system dependencies
RUN apt-get update && apt-get install -y \
    curl \
    zip \
    unzip \
    libcurl4 \
    libcurl4-openssl-dev \
    libgd-dev \ 
    libjpeg-dev \
    libonig-dev \
    libxml2-dev \
    libzip-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev

# Set up PHP to support GD
RUN docker-php-ext-configure gd --with-freetype --with-jpeg

RUN docker-php-ext-install -j$(nproc) gd
# Install PHP extensions
RUN docker-php-ext-install \
    pdo \
    pdo_mysql \
    curl \
    zip \
    mbstring \ 
    xml

# Download and install OpenCart
RUN curl -SL https://github.com/opencart/opencart/releases/download/3.0.3.8/opencart-3.0.3.8.zip -o opencart.zip \
    && unzip opencart.zip \
    && rm opencart.zip \
    && mv upload/.htaccess.txt .htaccess \
    && mv upload/* . \
    # Remove upload and  opencart-3.0.3.8 folder
    && rm -r upload \
    # Rename some file
    && mv config-dist.php config.php \
    && mv admin/config-dist.php admin/config.php \
    # Set owner ship
    && chown -R www-data:www-data . \
    && chmod 0777 config.php && chmod 0777 admin/config.php
# Enable Apache rewrite module
RUN a2enmod rewrite

# Copy custom php.ini if needed
# COPY php.ini /usr/local/etc/php/

# Expose port 80
EXPOSE 80

# Start Apache server
CMD ["apache2-foreground"]