FROM php:8.2-apache

# Install ekstensi Laravel yang dibutuhkan
RUN docker-php-ext-install pdo pdo_mysql

# Aktifkan mod_rewrite untuk Laravel
RUN a2enmod rewrite

# Salin semua file Laravel ke direktori Apache
COPY . /var/www/html

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
