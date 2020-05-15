FROM php:7.4-fpm 

RUN apt-get update \
  && apt-get install -y \
    cron \
    libfreetype6-dev \
    libicu-dev \
    libjpeg62-turbo-dev \
    libonig-dev \
    libpng-dev \
    libxslt1-dev \
    libzip-dev \
    openssh-server \
    openssh-client \
    rsync \
    supervisor

RUN docker-php-ext-configure \
  gd --with-freetype --with-jpeg

RUN docker-php-ext-install \
  bcmath \
  gd \
  intl \
  mbstring \
  pdo_mysql \
  soap \
  xsl \
  zip

RUN pecl install -o -f redis \
&&  rm -rf /tmp/pear \
&&  docker-php-ext-enable redis

RUN curl -sS https://getcomposer.org/installer | \
    php -- --install-dir=/usr/local/bin --filename=composer
    
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

RUN sed -i "s/^listen = .*/listen = 9000/" /usr/local/etc/php-fpm.d/www.conf

EXPOSE 9000

CMD ["/usr/bin/supervisord"]
