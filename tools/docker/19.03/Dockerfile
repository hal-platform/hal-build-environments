FROM halplatform/hal-build-environments:debian10-buildpack

RUN \
    apt-get update \
        && \
    apt-get install -y --no-install-recommends \
        apt-transport-https \
        && \
    rm -rf /var/lib/apt/lists/*

ENV DOCKER_VERSION "19.03.5"

RUN curl -L "https://download.docker.com/linux/debian/gpg" | apt-key add - \
        && \
    echo 'deb [arch=amd64] https://download.docker.com/linux/debian buster stable' > "/etc/apt/sources.list.d/docker.list" \
        && \
    apt-get update \
        && \
    apt-get install -y \
        "docker-ce=5:${DOCKER_VERSION}~3-0~debian-buster" \
        && \
    rm -rf /var/lib/apt/lists/*
