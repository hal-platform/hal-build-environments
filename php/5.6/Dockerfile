FROM halplatform/hal-build-environments:centos7-buildpack

################################################################################
# Import Remi Repository
################################################################################

RUN yum install -y \
    yum-utils \
    wget \
    epel-release \
        && \
        \
    rpm -Uvh http://rpms.remirepo.net/enterprise/remi-release-7.rpm \
        && \
    yum-config-manager -q --enable remi \
        && \
    yum-config-manager -q --enable remi-php56

################################################################################
# PHP
################################################################################

RUN yum install -y \
    php-fpm \
    php-cli \
    \
    php-bcmath \
    php-intl \
    php-mbstring \
    php-opcache \
    php-xml \
    \
    php-mcrypt \
    php-openssl \
    php-pecl-libsodium \
    \
    php-pdo \
    php-mysql \
    php-mssql \
    php-pgsql \
    \
    php-ldap \
    php-soap \
    \
    php-pecl-apcu \
    php-pecl-memcache \
    php-pecl-xdebug \
    && \
    yum clean all

RUN sed -i "s/;date.timezone =.*/date.timezone = UTC/" /etc/php.ini

ENV COMPOSER_NO_INTERACTION 1
ENV COMPOSER_VERSION        1.5.2

RUN curl -LO "https://composer.github.io/installer.sha384sum" \
        && \
    curl -LO "https://getcomposer.org/installer" \
        && \
    echo "$(cat installer.sha384sum installer)" | sha384sum -c - \
        && \
    php "./installer" -- \
        --install-dir="/usr/local/bin" \
        --filename="composer" \
        --version="${COMPOSER_VERSION}" \
        && \
    rm -f \
        "installer" \
        "installer.sig"
