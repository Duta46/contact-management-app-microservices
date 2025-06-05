FROM php:8.2-apache

# Install dependencies & Composer
RUN apt-get update && apt-get install -y \
    unzip \
    curl \
    git \
    zip \
    && curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

# Install ekstensi Laravel yang dibutuhkan
RUN docker-php-ext-install pdo pdo_mysql

# Aktifkan mod_rewrite untuk Laravel
RUN a2enmod rewrite


# Set permission
RUN chown -R www-data:www-data /var/www/html \
    && chmod -R 755 /var/www/html

# Ubah DocumentRoot ke folder 'public'
RUN sed -i 's|DocumentRoot /var/www/html|DocumentRoot /var/www/html/public|' /etc/apache2/sites-available/000-default.conf

# Pastikan direktori public dapat diakses
RUN echo "<Directory /var/www/html/public>\n\
    AllowOverride All\n\
    Require all granted\n\
    </Directory>" >> /etc/apache2/apache2.conf
