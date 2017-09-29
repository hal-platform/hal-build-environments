FROM halplatform/hal-build-environments:centos7-buildpack

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN rpm -Uvh \
    "https://packages.erlang-solutions.com/erlang-solutions-1.0-1.noarch.rpm"

ENV ERLANG_VERSION 19.3
ENV ELIXIR_VERSION 1.4.5

ENV ELIXIR_DOWNLOAD_URL="https://github.com/elixir-lang/elixir/releases/download/v${ELIXIR_VERSION}/Precompiled.zip"
ENV ELIXIR_DOWNLOAD_SHA256="a740e634e3c68b1477e16d75a0fd400237a46c62ceb5d04551dbc46093a03f98"

RUN yum --assumeyes install \
        "esl-erlang-${ERLANG_VERSION}" \
        && \
    yum clean all

RUN \
    curl -fSL -o elixir-precompiled.zip "${ELIXIR_DOWNLOAD_URL}" \
        && \
    echo "${ELIXIR_DOWNLOAD_SHA256}" "elixir-precompiled.zip" | sha256sum -c - \
        && \
    unzip -d "/usr/local" "elixir-precompiled.zip" \
        && \
    rm "elixir-precompiled.zip"
