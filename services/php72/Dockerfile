ARG PHP_VERSION
FROM ${PHP_VERSION}

ARG TZ
ARG CONTAINER_PACKAGE_URL

RUN if [ "${CONTAINER_PACKAGE_URL}" != "" ]; then \
        sed -i "s/dl-cdn.alpinelinux.org/${CONTAINER_PACKAGE_URL}/g" /etc/apk/repositories; \
    fi

RUN apk update

# Extension
RUN docker-php-ext-install mysqli pdo pdo_mysql
RUN docker-php-ext-enable pdo_mysql

# Composer
RUN php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer

# Git
RUN apk add --no-cache bash git openssh
RUN git config --global user.name "yourname"
RUN git config --global user.email "youremail"

WORKDIR /home/webroot