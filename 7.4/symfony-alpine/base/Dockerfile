ARG ALPINE_VERSION

FROM php:7.4-fpm-alpine$ALPINE_VERSION

# install require package
RUN apk add \
        icu-dev libxml2-dev gmp-dev \
        m4 libbz2 perl autoconf autoconf dpkg-dev dpkg libmagic file binutils libgomp libatomic \
        libgphobos gmp mpfr4 mpc1 gcc musl-dev libc-dev g++ make re2c \
        libsodium libsodium-dev \
        libpng-dev freetype-dev libjpeg-turbo-dev libwebp \
        ca-certificates ffmpeg libzip-dev \
        curl wget tar tzdata xz \
    && rm -rf /var/cache/apk/* /tmp/* \
    && echo -e "\033[42;37m Package Install Completed :).\033[0m\n"

RUN pecl install redis

RUN docker-php-ext-configure intl \
    && docker-php-ext-configure sodium \
    && docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install opcache bcmath sodium xml gmp tokenizer pcntl zip mysqli pdo pdo_mysql \
    && echo -e "\033[42;37m PHP ext Install Completed :).\033[0m\n"

RUN echo 'alias ll="ls -l"' >> ~/.bashrc

WORKDIR /var/www

COPY composer.phar /usr/local/bin/composer
RUN chmod +x /usr/local/bin/composer
#ADD symfony.ini $PHP_INI_DIR/conf.d/symfony.ini

CMD ["php-fpm"]

EXPOSE 9000
