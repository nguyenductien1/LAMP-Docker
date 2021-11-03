FROM php:7.3-fpm

# Install apcache, mysqli, pdo_mysql, memcached

RUN docker-php-ext-install mysqli
RUN docker-php-ext-install pdo_mysql
RUN mkdir -p /home/sites


WORKDIR /home/sites/:

EXPOSE 9000

# CMD [ "httpd-foreground"]
