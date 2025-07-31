# Étape 1 : Choisir une image PHP officielle avec Apache
FROM php:8.2-apache

# Étape 2 : Installer les extensions nécessaires à Laravel
RUN apt-get update && apt-get install -y \
    git curl zip unzip libpng-dev libonig-dev libxml2-dev libzip-dev \
    && docker-php-ext-install pdo pdo_mysql mbstring exif pcntl bcmath gd zip

# Étape 3 : Activer le module Apache pour Laravel
RUN a2enmod rewrite

# Étape 4 : Installer Composer
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

# Étape 5 : Mettre Laravel dans le dossier Apache
WORKDIR /var/www/html
COPY . /var/www/html

# Étape 6 : Donner les droits au serveur
RUN chown -R www-data:www-data /var/www/html \
    && chmod -R 755 /var/www/html

# Étape 7 : Installer les dépendances Laravel
RUN composer install --no-dev --optimize-autoloader

# Étape 8 : Exposer le port 80
EXPOSE 80
