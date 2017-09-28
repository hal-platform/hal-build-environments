FROM python:3.6.2-jessie

RUN \
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
    pip install awscli
