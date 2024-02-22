FROM php:8.3-fpm

# Setup container user with same ID as local to avoid ownerwhip issue
ARG uid
ARG username=php
ARG password=123
ARG root_password=123

RUN usermod --password $(openssl passwd $root_password) root && \
    useradd $username \
        --create-home \
        --groups sudo \
        --uid $uid \
        --home-dir /home/$username \
        --password $(openssl passwd $password) && \
    apt-get update && \
    apt-get install -y sudo unzip curl wget libmcrypt-dev git zsh libzip-dev libpng-dev zip libfreetype6-dev libjpeg62-turbo-dev libicu-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    curl -sS https://getcomposer.org/installer -o composer-setup.php && \
    php composer-setup.php --install-dir=/usr/local/bin --filename=composer && \
    rm composer-setup.php && \
    composer --version && \
    docker-php-ext-install zip pdo_mysql && \
    docker-php-ext-configure gd --with-freetype --with-jpeg && \
    docker-php-ext-install -j$(nproc) gd exif intl

# Change shell to zsh
RUN chsh -s $(which zsh) $username

# Change to the specified user
USER $username

# install oh my zsh
RUN wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true

# Copy custom PHP INI settings
COPY php.ini /usr/local/etc/php/php.ini

# Set the working directory
WORKDIR /webroot/app

