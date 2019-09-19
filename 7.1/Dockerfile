FROM ubuntu:latest

RUN apt-get update

RUN apt-get install -y software-properties-common

RUN apt-get install -y language-pack-en-base

RUN apt-get install -y iputils-ping

RUN LC_ALL=en_US.UTF-8 add-apt-repository ppa:ondrej/php

RUN apt-get update && apt-get upgrade -y

RUN echo "Europe/Moscow" > /etc/timezone
RUN apt-get install tzdata -y
RUN dpkg-reconfigure -f noninteractive tzdata

RUN apt-get install -y php7.1 php7.1-cli php7.1-common php7.1-json php7.1-opcache php7.1-mysql php7.1-mbstring php7.1-mcrypt php7.1-zip php7.1-fpm php7.1-dev php7.1-pgsql php7.1-amqp php7.1-xml php7.1-intl php7.1-curl php7.1-bcmath php7.1-gd
php7.1-imagick

RUN pecl install timezonedb \
    && echo "extension=timezonedb.so" > /etc/php/7.1/mods-available/timezonedb.ini \
    && phpenmod timezonedb

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    && php -r "unlink('composer-setup.php');"

RUN apt-get install -y git

RUN  apt-get install -y supervisor

RUN mkdir /run/php

WORKDIR /app

EXPOSE 9000

CMD ["php-fpm7.1", "--nodaemonize"]

