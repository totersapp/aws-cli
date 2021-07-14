FROM php:7.4-alpine

# Install dev dependencies
RUN apk add --no-cache --virtual .build-deps \
    $PHPIZE_DEPS \
    curl-dev \
    imagemagick-dev \
    libtool \
    libxml2-dev \
    postgresql-dev \
    sqlite-dev

# Install production dependencies
RUN apk add --no-cache \
    bash \
    curl \
    freetype-dev \
    g++ \
    jq \
    gcc \
    git \
    imagemagick \
    libc-dev \
    libjpeg-turbo-dev \
    libpng-dev \
    libzip-dev \
    make \
    mysql-client \
    nodejs \
    nodejs-npm \
    oniguruma-dev \
    yarn \
    openssh-client \
    postgresql-libs \
    rsync \
    zlib-dev \
    php-phpdbg

# Install PECL and PEAR extensions
RUN pecl install \
    imagick \
    redis

# Install and enable php extensions
RUN docker-php-ext-enable \
    imagick \
    redis

# Configure php extensions
RUN docker-php-ext-configure gd --with-freetype --with-jpeg

RUN docker-php-ext-install \
    bcmath \
    calendar \
    curl \
    exif \
    gd \
    iconv \
    mbstring \
    pdo \
    pdo_mysql \
    pdo_pgsql \
    pdo_sqlite \
    pcntl \
    tokenizer \
    xml \
    zip
# Install composer

ENV COMPOSER_HOME /composer
ENV PATH ./vendor/bin:/composer/vendor/bin:$PATH
ENV COMPOSER_ALLOW_SUPERUSER 1
RUN curl -s https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer

# Install PHP_CodeSniffer
RUN composer global require "squizlabs/php_codesniffer=*"

# Cleanup dev dependencies
RUN apk del -f .build-deps

# Increase php memory limit
RUN sed -i -e "s/^ *memory_limit.*/memory_limit = 512M/g" /usr/local/etc/php/php.ini-production
RUN sed -i -e "s/^ *memory_limit.*/memory_limit = 512M/g" /usr/local/etc/php/php.ini-development
RUN echo "memory_limit=512M" > /usr/local/etc/php/conf.d/memory-limit-php.ini

# Install aws-cli
RUN apk add --no-cache \
        python3 \
        py3-pip \
    && pip3 install --upgrade pip \
    && pip3 install \
        awscli \
    && apk -v --purge del py3-pip \
    && rm -rf /var/cache/apk/*

# Setup working directory
WORKDIR /var/www