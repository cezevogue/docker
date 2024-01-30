FROM php:8.1-apache


RUN echo "ServerName 127.0.0.1" >> /etc/apache2/apache2.conf

ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

RUN chmod +x /usr/local/bin/install-php-extensions && \
    install-php-extensions pdo_mysql intl zip

RUN curl -sSk https://getcomposer.org/installer | php -- --disable-tls && \
   mv composer.phar /usr/local/bin/composer

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y git

COPY . /var/www/

COPY ./docker/vhosts/vhosts.conf /etc/apache2/sites-available/000-default.conf

RUN git clone https://github.com/cezevogue/final_wanted.git | bash

RUN cd final_wanted && composer install




WORKDIR /var/www/

CMD ["php", "-S", "127.0.0.1:80", "-t", "/final_wanted/public"]

ENTRYPOINT ["bash", "./docker/docker.sh"]

EXPOSE 80