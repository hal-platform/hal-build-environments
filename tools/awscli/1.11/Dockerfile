FROM python:3.6.2-jessie

RUN echo '\
deb http://deb.debian.org/debian/ jessie main contrib non-free\n\
deb-src http://deb.debian.org/debian/ jessie main contrib non-free\n\
deb http://security.debian.org/ jessie/updates main contrib non-free\n\
deb-src http://security.debian.org/ jessie/updates main contrib non-free\n\
' > "/etc/apt/sources.list"

ENV AWSCLI_VERSION 1.11.161

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
