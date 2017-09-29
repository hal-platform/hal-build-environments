FROM halplatform/hal-build-environments:centos7-buildpack

ENV PATH /usr/local/bin:$PATH

# http://bugs.python.org/issue19846
# > At the moment, setting "LANG=C" on a Linux system *fundamentally breaks Python 3*, and that's not OK.
ENV LANG C.UTF-8

ENV PYTHON_VERSION     3.6.2
ENV PYTHON_PIP_VERSION 9.0.1

ENV GPG_KEY 0D96DF4D4110E5C43FBFB17F2D347EA6AA65421D

RUN set -x \
        && \
    mkdir -p "/usr/src/python" \
        && \
    curl -SL "https://www.python.org/ftp/python/${PYTHON_VERSION}/Python-${PYTHON_VERSION}.tar.xz" \
        -o "python.tar.xz" \
        && \
    curl -SL "https://www.python.org/ftp/python/${PYTHON_VERSION}/Python-${PYTHON_VERSION}.tar.xz.asc" \
        -o "python.tar.xz.asc" \
        && \
    gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "${GPG_KEY}" \
        && \
    gpg --verify "python.tar.xz.asc" \
        && \
    tar -xJC "/usr/src/python" --strip-components=1 -f "python.tar.xz" \
        && \
    rm "python.tar.xz*" \
        && \
    cd "/usr/src/python" \
        && \
    ./configure --enable-shared \
        && \
    make -j$(nproc) \
        && \
    make altinstall \
        && \
    echo "/usr/local/lib/" > "/etc/ld.so.conf.d/local.conf" && ldconfig \
        && \
    curl -SL 'https://bootstrap.pypa.io/get-pip.py' | python \
        && \
    pip3.6 install --no-cache-dir --upgrade --ignore-installed pip=="${PYTHON_PIP_VERSION}" \
        && \
    find /usr/local -depth \
        \( \
            \( -type d -a \( -name test -o -name tests \) \) \
                -o \
            \( -type f -a \( -name '*.pyc' -o -name '*.pyo' \) \) \
        \) -exec rm -rf '{}' + \
        && \
    rm -rf "/usr/src/python"

RUN pip install --no-cache-dir virtualenv
