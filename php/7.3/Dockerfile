FROM halplatform/hal-build-environments:debian9-buildpack

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
    echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" | tee "/etc/apt/sources.list.d/php7.3.list" \
        && \
    rm -rf /var/lib/apt/lists/*

################################################################################
# PHP
################################################################################

RUN \
    apt-get update && \
    apt-get  install -y \
        php7.3 \
        php7.3-cli \
        \
        php7.3-bcmath \
        php7.3-curl \
        php7.3-intl \
        php7.3-mbstring \
        php7.3-opcache \
        php7.3-xml \
        php7.3-zip \
        \
        php7.3-pdo \
        php7.3-mysql \
        php7.3-pgsql \
        php7.3-sqlite3 \
        \
        php7.3-ldap \
        php7.3-soap \
        \
        php7.3-apcu \
        php7.3-memcached \
        php7.3-phpdbg \
        php7.3-xdebug \
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
