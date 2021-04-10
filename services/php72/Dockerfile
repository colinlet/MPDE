ARG PHP_VERSION
FROM ${PHP_VERSION}

ARG CONTAINER_PACKAGE_URL
ARG TZ
ARG PHP_EXTENSIONS

#RUN apk --no-cache add tzdata \
#    && cp "/usr/share/zoneinfo/$TZ" /etc/localtime \
#    && echo "$TZ" > /etc/timezone

RUN if [ $CONTAINER_PACKAGE_URL ] ; then sed -i "s/dl-cdn.alpinelinux.org/${CONTAINER_PACKAGE_URL}/g" /etc/apk/repositories ; fi

COPY ./extensions /tmp/extensions
WORKDIR /tmp/extensions
RUN chmod +x install.sh \
    && sh install.sh \
    && rm -rf /tmp/extensions

ADD ./extensions/install-php-extensions  /usr/local/bin/
RUN chmod uga+x /usr/local/bin/install-php-extensions

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