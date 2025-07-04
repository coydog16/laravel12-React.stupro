FROM php:8.3-fpm
WORKDIR /var/www
ADD . /var/www

# permission
RUN chown -R www-data:www-data /var/www

# install composer
RUN cd /usr/bin && curl -s http://getcomposer.org/installer | php && ln -s /usr/bin/composer.phar /usr/bin/composer

# install packages
RUN apt-get update \
  && apt-get install -y \
  gcc \
  make \
  git \
  unzip \
  vim \
  libpng-dev \
  libjpeg-dev \
  libfreetype6-dev \
  libmcrypt-dev \
  libpq-dev \
  curl \
  gnupg \
  openssl \
  && docker-php-ext-install pdo_pgsql pgsql \
  && docker-php-ext-configure gd --with-freetype --with-jpeg \
  && docker-php-ext-install -j$(nproc) gd

# Add php.ini
COPY php.ini /usr/local/etc/php/

# install stable node and latest npm
RUN apt-get update \
    && apt-get install -y curl \
    && curl -fsSL https://deb.nodesource.com/setup_22.x | bash - \
    && apt-get install -y nodejs 
# install node packages
RUN npm install -g n
RUN n stable
RUN npm update -g npm