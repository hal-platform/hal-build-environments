FROM halplatform/hal-build-environments:debian9-buildpack

RUN \
    apt-get update \
        && \
    apt-get install -y --no-install-recommends \
        apt-transport-https \
        && \
    rm -rf /var/lib/apt/lists/*

ENV DOCKER_VERSION "18.03"

RUN curl -L "https://download.docker.com/linux/debian/gpg" | apt-key add - \
        && \
    echo 'deb [arch=amd64] https://download.docker.com/linux/debian jessie stable' > "/etc/apt/sources.list.d/docker.list" \
        && \
    apt-get update \
        && \
    apt-get install -y \
        "docker-ce=${DOCKER_VERSION}.0~ce-0~debian" \
        && \
    rm -rf /var/lib/apt/lists/*
