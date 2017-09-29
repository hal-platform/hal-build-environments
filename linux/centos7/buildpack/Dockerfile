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
    yum -y install \
        ImageMagick \
        ImageMagick-devel \
        bzip2-devel \
        glib2-devel \
        libcurl-devel \
        libevent-devel \
        libffi-devel \
        libjpeg-devel \
        libxml2-devel \
        libxslt-devel \
        libyaml-devel \
        mysql-devel \
        ncurses-devel \
        openssl-devel \
        postgresql-devel \
        readline-devel \
        sqlite-devel \
        zlib-devel \
        && \
    yum clean all
