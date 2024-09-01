FROM php:8.3-fpm-alpine

# Instalar pacotes e dependências necessários
RUN apk add --no-cache \
    bash \
    linux-headers \
    curl \
    libpng-dev \
    libzip-dev \
    zlib-dev \
    postgresql-dev \
    libxml2-dev \
    oniguruma-dev \
    nodejs \
    npm \
    autoconf \
    automake \
    g++ \
    make

# Instalar extensões PHP
RUN docker-php-ext-install gd zip pdo pdo_pgsql

# Instalar e habilitar o Xdebug
RUN pecl install -o -f xdebug \
    && docker-php-ext-enable xdebug

RUN echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_handler=dbgp" >>  /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_port=9000" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_autostart=on" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_connect_back=on" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.idekey=docker" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_log=/app/storage/logs/xdebug.log" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.default_enable=on" >> /usr/local/etc/php/conf.d/xdebug.ini

# Copiar o Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
 
# Copiar o arquivo php.ini
COPY ./dockerfiles/php/php.ini /usr/local/etc/php/php.ini

WORKDIR /var/www

EXPOSE 9000
