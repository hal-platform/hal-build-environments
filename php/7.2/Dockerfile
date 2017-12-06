FROM halplatform/hal-build-environments:centos7-buildpack

RUN \
    yum install -y \
        yum-utils \
        wget \
        epel-release \
        \
        && \
    rpm -Uvh http://rpms.remirepo.net/enterprise/remi-release-7.rpm \
        && \
    yum-config-manager -q --enable remi \
        && \
    yum-config-manager -q --enable remi-php72

################################################################################
# PHP
################################################################################

RUN \
    yum install -y \
        php-fpm \
        php-cli \
        \
        php-bcmath \
        php-intl \
        php-mbstring \
        php-opcache \
        php-xml \
        php-zip \
        \
        php-openssl \
        php-sodium \
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
        php-pecl-memcached \
        php-pecl-xdebug \
        \
        && \
    yum clean all

################################################################################
# Composer
################################################################################

ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_NO_INTERACTION  1
ENV COMPOSER_VERSION         1.5.2

RUN curl -LO "https://composer.github.io/installer.sha384sum" \
        && \
    curl -L "https://getcomposer.org/installer" \
        -o "composer-setup.php" \
        && \
    ls -hal && \
    echo "$(cat installer.sha384sum composer-setup.php)" | sha384sum -c - \
        && \
    php "composer-setup.php" -- \
        --install-dir="/usr/local/bin" \
        --filename="composer" \
        --version="${COMPOSER_VERSION}" \
        && \
    rm -f \
        "composer-setup.php" \
        "installer.sig"
