FROM centos:7.4.1708

RUN \
    yum -y update \
        && \
    yum -y install \
        epel-release \
        \
        cvs git mercurial subversion \
        \
        curl wget \
        \
        bzip2 tar zip unzip \
        \
        && \
    yum -y groupinstall \
        'Development Tools' \
        && \
    yum -y install
        ImageMagick \
        bzip2-devel \
        libcurl-devel \
        libevent-devel \
        libffi-devel \
        glib2-devel \
        libjpeg-devel \
        ImageMagick-devel \
        mysql-devel \
        ncurses-devel \
        postgresql-devel \
        readline-devel \
        sqlite-devel \
        openssl-devel \
        libxml2-devel \
        libxslt-devel \
        libyaml-devel \
        zlib-devel \
        && \
    yum clean all
