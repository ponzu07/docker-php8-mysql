FROM php:8-apache

# Timezone
ENV TZ=Asia/Tokyo
RUN echo $TZ > /etc/timezone
RUN dpkg-reconfigure -f noninteractive tzdata
RUN echo date.timezone = $TZ > /usr/local/etc/php/conf.d/docker-php-ext-timezone.ini

RUN  apt-get update \
  && apt-get upgrade -y \
  && apt-get autoremove -y \
  && apt-get install -yq \
  libssl-dev \
  openssl \
  && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

RUN docker-php-ext-install \
  bcmath \
  ctype \
  fileinfo \
  json \
  mbstring \
  pdo \
  pdo_mysql \
  tokenizer \
  xml

RUN a2enmod rewrite
RUN a2enmod ssl
RUN a2ensite default-ssl
RUN echo "ServerName docker" >> /etc/apache2/apache2.conf

RUN usermod -u 1000 www-data
RUN chown www-data:1000 -R /var/www/

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]