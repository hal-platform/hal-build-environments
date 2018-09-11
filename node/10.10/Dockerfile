FROM halplatform/hal-build-environments:debian9-buildpack

ENV NODE_VERSION "10.10.0"
ENV YARN_VERSION "1.9.4"

ENV NODE_DEB_URL "https://deb.nodesource.com/node_10.x/pool/main/n/nodejs/nodejs_${NODE_VERSION}-1nodesource1_amd64.deb"

RUN apt-get update && apt-get install -y apt-transport-https \
        && \
    echo ; echo "Downloading ${NODE_DEB_URL}" ; echo \
        && \
    curl -sLo nodejs.deb "${NODE_DEB_URL}" \
        && \
    apt-get install -y ./nodejs.deb \
        && \
    rm nodejs.deb && rm -rf /var/lib/apt/lists/*

RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee "/etc/apt/sources.list.d/yarn.list" \
        && \
    curl -sS "https://dl.yarnpkg.com/debian/pubkey.gpg" | apt-key add - \
        && \
    apt-get update \
        && \
    apt-get install -y \
        "yarn=${YARN_VERSION}-1" \
        && \
    rm -rf /var/lib/apt/lists/*
