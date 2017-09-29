FROM halplatform/hal-build-environments:centos7-buildpack

ENV PATH /usr/local/bin:$PATH

# http://bugs.python.org/issue19846
# > At the moment, setting "LANG=C" on a Linux system *fundamentally breaks Python 3*, and that's not OK.
ENV LANG C.UTF-8

ENV PYTHON_VERSION     2.7.14
ENV PYTHON_PIP_VERSION 7.1.2

ENV GPG_KEY C01E1CAD5EA2C4F0B8E3571504C367C218ADD4FF

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
    ./configure \
        && \
    make -j$(nproc) \
        && \
    make install \
        && \
    ldconfig \
        && \
    curl -SL 'https://bootstrap.pypa.io/get-pip.py' | python2 \
        && \
    pip2.7 install --no-cache-dir --upgrade pip=="${PYTHON_PIP_VERSION}" \
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
