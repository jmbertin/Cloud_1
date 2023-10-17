FROM php:8.1.20RC1-fpm-alpine3.16

# Install dependencies
RUN apk update \
    && apk add --no-cache \
    curl \
    less \
    git \
    mysql-client \
    mariadb-connector-c

# Install PHP extensions
RUN docker-php-ext-install mysqli pdo_mysql

# Download wp-cli, set permissions, and move to path.
RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
    && chmod +x wp-cli.phar \
    && mv wp-cli.phar /usr/local/bin/wp

# Verify installation
RUN wp --info

EXPOSE 9000

CMD ["php-fpm"]
