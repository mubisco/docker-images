FROM alpine:3.21

RUN apk update && apk add bash curl git neovim zip zsh;

RUN apk add --no-cache php84 \
  php84-bcmath \
  php84-cli \
  php84-ctype \
  php84-curl \
  php84-dom \
  php84-fpm \
  php84-gd \
  php84-iconv \
  php84-intl \
  php84-mbstring \
  php84-mysqlnd \
  php84-opcache \
  php84-openssl \
  php84-pdo \
  php84-pdo_mysql \
  php84-phar \
  php84-posix \
  php84-session \
  php84-simplexml \
  php84-soap \
  php84-sodium \
  php84-tokenizer \
  php84-xml \
  php84-xmlwriter \
  php84-xdebug \
  php84-zip \
  php84-zlib

COPY ./xdebug-custom.ini /etc/php84/conf.d/99_custom_xdebug.ini

ENV COMPOSER_ALLOW_SUPERUSER=1
COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

RUN mkdir -p /usr/local/bin/ \
  && curl -sS https://get.symfony.com/cli/installer | bash \
  && mv /root/.symfony5/bin/symfony /usr/local/bin/symfony

RUN mkdir -p /etc/php/8.4/fpm
COPY ./php.ini /etc/php/8.4/cli/conf.d/custom-php.ini
RUN ln -s /usr/bin/php84 /usr/bin/php

RUN adduser \
  --disabled-password \
  --uid=1000 \
  --shell=/bin/zsh webdev

WORKDIR /app
USER webdev

RUN sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

# Aliases
RUN echo "\
  alias php='php84' \
  alias sf='symfony' \
  alias sfc='symfony console' \
  alias scc='php /app/bin/console cache:clear' \
  alias sft='php /app/vendor/bin/phpunit' \
  alias cmp='composer' \
  alias v='nvim' \
  " >> /home/webdev/.zshrc
