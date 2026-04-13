
FROM php:8.1-fpm

# Fail fast and print commands (helps debugging)
SHELL ["/bin/sh", "-lc"]

RUN set -eux; \
  apt-get update; \
  apt-get install -y --no-install-recommends \
    git unzip ca-certificates \
    libzip-dev libicu-dev libxml2-dev libxslt1-dev \
    libpng-dev libjpeg62-turbo-dev libfreetype6-dev \
    libonig-dev libcurl4-openssl-dev default-mysql-client \
    pkg-config \
    coreutils \
  ; \
  rm -rf /var/lib/apt/lists/*

# Sanity-check that docker-php scripts exist (if not, base image is wrong)
RUN set -eux; \
  command -v docker-php-ext-configure; \
  command -v docker-php-ext-install

# PHP extensions required by Magento
RUN set -eux; \
  docker-php-ext-configure gd --with-freetype --with-jpeg; \
  JOBS="$(getconf _NPROCESSORS_ONLN 2>/dev/null || echo 1)"; \
  docker-php-ext-install -j"${JOBS}" \
    bcmath intl pdo_mysql soap xsl zip sockets opcache gd

# Composer
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

COPY php.ini /usr/local/etc/php/conf.d/zz-magento.ini
WORKDIR /var/www/html
