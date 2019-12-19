FROM halplatform/hal-build-environments:debian10-buildpack

RUN \
    apt-get update && \
    apt-get install -y \
        lsb-release \
        apt-transport-https \
        ca-certificates \
        \
        && \
    wget -O "/etc/apt/trusted.gpg.d/php.gpg" "https://packages.sury.org/php/apt.gpg" \
        && \
    echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" | tee "/etc/apt/sources.list.d/php7.4.list" \
        && \
    rm -rf /var/lib/apt/lists/*

################################################################################
# PHP
################################################################################

RUN \
    apt-get update && \
    apt-get  install -y \
        php7.4 \
        php7.4-cli \
        \
        php7.4-bcmath \
        php7.4-curl \
        php7.4-intl \
        php7.4-mbstring \
        php7.4-opcache \
        php7.4-xml \
        php7.4-zip \
        \
        php7.4-pdo \
        php7.4-mysql \
        php7.4-pgsql \
        php7.4-sqlite3 \
        \
        php7.4-ldap \
        php7.4-soap \
        \
        php7.4-apcu \
        php7.4-memcached \
        php7.4-phpdbg \
        php7.4-xdebug \
        && \
    rm -rf /var/lib/apt/lists/*

RUN \
    apt-get update && \
    apt-cache search php

################################################################################
# Composer
################################################################################

ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_NO_INTERACTION  1
ENV COMPOSER_VERSION         1.8.0

RUN curl -LO "https://composer.github.io/installer.sha384sum" \
        && \
    curl -L "https://getcomposer.org/installer" \
        -o "composer-setup.php" \
        && \
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
