FROM php:7.4-fpm

# Instalando pacotes complementares
RUN apt-get update \
 && apt-get install -y libpq-dev \
 && docker-php-ext-install pdo pdo_pgsql pdo_mysql opcache

# Instalando XDebug
RUN yes | pecl install xdebug \
 && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini \
 && echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/xdebug.ini \
 && echo "xdebug.remote_autostart=off" >> /usr/local/etc/php/conf.d/xdebug.ini

# Limpado cache da imagem
RUN apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Use the default production configuration
RUN mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"

# Override with custom opcache settings
COPY data/php.ini $PHP_INI_DIR/conf.d/

WORKDIR /var/www