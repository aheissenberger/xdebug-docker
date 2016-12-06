FROM php:5.6-apache
# based on debian:jessie
# https://github.com/docker-library/php/blob/master/5.6/apache/Dockerfile

# Download requirements
RUN apt-get update -qq && \
    pecl install xdebug \
        && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini \
        && echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/xdebug.ini \
        && echo "xdebug.remote_autostart=off" >> /usr/local/etc/php/conf.d/xdebug.ini

# Cleanup apt/dpkg
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# fix write problems with mounted volumes from host
RUN usermod -u 1000 www-data

# set permissions
RUN cd /var/www && \
    chown -R www-data:www-data /var/www

# PHP configuration 
COPY php.ini /usr/local/etc/php/php.ini

# Typo3 Apache module
COPY apache.conf /etc/apache2/conf-enabled/apache.conf

EXPOSE 80