# Use the official PHP 7.4 Apache base image
FROM php:7.4-apache

# Set the working directory to /var/www/html
WORKDIR /var/www/html

# Install system dependencies
RUN apt-get update && apt-get install -y \
    curl \
    libcurl4 \
    libcurl4-openssl-dev \
    libzip-dev \
    zip \
    unzip \
    libpng-dev \
    libonig-dev \
    libxml2-dev

# Install PHP extensions
RUN docker-php-ext-install \
    pdo \
    pdo_mysql \
    curl \
    zip \
    gd \
    mbstring \ 
    xml

# Download and install OpenCart
RUN curl -SL https://github.com/opencart/opencart/releases/download/3.0.3.8/opencart-3.0.3.8.zip -o opencart.zip \
    && unzip opencart.zip \
    && rm opencart.zip \
    && mv upload/* . \
    && rm -r upload \
    && chown -R www-data:www-data .

# Create symbolic links from config.php to config-dist.php
RUN ln -sf config-dist.php config.php && \
    ln -sf config-dist.php admin/config.php
    
# Enable Apache rewrite module
RUN a2enmod rewrite

# Copy custom php.ini if needed
# COPY php.ini /usr/local/etc/php/

# Expose port 80
EXPOSE 80

# Start Apache server
CMD ["apache2-foreground"]