FROM halplatform/hal-build-environments:centos7-buildpack

ENV NODE_VERSION "8.10.0"
ENV NODE_SETUP   "setup_8.x"
ENV NODE_URL     "https://rpm.nodesource.com/${NODE_SETUP}"
ENV YARN_VERSION "1.5.1"

RUN curl -sLO "${NODE_URL}" \
        && \
    chmod +x "${NODE_SETUP}" \
        && \
    "./${NODE_SETUP}"

RUN yum install -y \
    "nodejs-${NODE_VERSION}"

RUN curl -sL \
        "https://dl.yarnpkg.com/rpm/yarn.repo" \
        --output "/etc/yum.repos.d/yarn.repo" \
        && \
    yum install -y \
        "yarn-${YARN_VERSION}"
