FROM php:7.3-fpm-alpine

RUN apk add --no-cache \
        $PHPIZE_DEPS \
        curl-dev \
        imagemagick-dev \
        libtool \
        libzip-dev \
        libxml2-dev \
        postgresql-dev \
        sqlite-dev \
    && apk --update --no-cache add p7zip \
    && apk add --no-cache \
        curl \
        git \
        imagemagick \
        mysql-client \
        postgresql-libs \
        libintl \
        icu \
        icu-dev \
        freetype-dev \
        libjpeg-turbo-dev \
        libpng-dev \
    && pecl install imagick \
    && docker-php-ext-enable imagick \
    && docker-php-ext-install \
        curl \
        iconv \
        mbstring \
        pdo \
        pdo_mysql \
        pdo_pgsql \
        pdo_sqlite \
        pcntl \
        tokenizer \
        xml \
        zip \
        intl \
        gd \
    && curl -s https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer

RUN docker-php-ext-install gd
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install -j$(nproc) gd

RUN apk add --no-cache icu-dev libxml2-dev \
    && docker-php-ext-configure intl --enable-intl \
    && docker-php-ext-configure soap --enable-soap \
    && docker-php-ext-install intl \
    && docker-php-ext-install soap

#VOLUME [ "/sys/fs/cgroup" ]
COPY entry.sh /entry.sh
RUN chmod 755 /entry.sh
CMD ["/entry.sh"]