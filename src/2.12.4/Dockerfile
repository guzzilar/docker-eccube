FROM php:5.6-apache

LABEL maintainer "Guzzilar"

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV APACHE_RUN_DIR /var/run/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2

RUN apt-get update && apt-get install -y --force-yes \
    libpq-dev \
    unzip

RUN docker-php-ext-install pdo pdo_pgsql pgsql

# Add INSTALL.sh.
COPY ./bin/install /var/www/bin/install
RUN chmod +x /var/www/bin/install

# WAIT-FOR-IT.sh.
ADD ./bin/wait-for-it /var/www/bin/wait-for-it
RUN chmod +x /var/www/bin/wait-for-it

# Apache configuration
RUN mkdir -p $APACHE_RUN_DIR $APACHE_LOCK_DIR $APACHE_LOG_DIR
RUN a2enmod rewrite
RUN chown www-data:www-data -R /var/www/html/

EXPOSE 80
