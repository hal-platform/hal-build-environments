FROM halplatform/hal-build-environments:centos7-buildpack

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN rpm -Uvh \
    "https://packages.erlang-solutions.com/erlang-solutions-1.0-1.noarch.rpm"

ENV ERLANG_VERSION 18.3
ENV ELIXIR_VERSION 1.2.6

ENV ELIXIR_DOWNLOAD_URL="https://github.com/elixir-lang/elixir/releases/download/${ELIXIR_VERSION}/Precompiled.zip"
ENV ELIXIR_DOWNLOAD_SHA256="bb4324eb7c9568fa30f0f2ed3c1b86ebbd5251f7c820f1beb0e5eed5fb8a9729"

RUN yum install -y \
        "esl-erlang-${ERLANG_VERSION}" \
        && \
    yum clean all

RUN \
    curl -fSL -o elixir-precompiled.zip "${ELIXIR_DOWNLOAD_URL}" \
        && \
    echo "${ELIXIR_DOWNLOAD_SHA256}" "elixir-precompiled.zip" | sha256sum -c - \
        && \
    unzip -d "/usr/local" "elixir-precompiled.zip" \
