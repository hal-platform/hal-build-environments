FROM python:3.6.2-stretch

ENV AWSCLI_VERSION 1.14.70

RUN \
    curl -Lo "yq" "https://github.com/mikefarah/yq/releases/download/1.14.0/yq_linux_amd64" \
        && chmod +x yq \
        && mv yq /usr/bin/yq \
        && \
    apt-get update \
        && \
    apt-get install -y --no-install-recommends \
        groff \
        less \
        jq \
        zip unzip \
        && \
    rm -rf /var/lib/apt/lists/* \
        && \
    pip install awscli=="${AWSCLI_VERSION}"
