FROM python:3.6.2-stretch

ENV AWSCLI_VERSION 1.16.306
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
    pip install awscli=="${AWSCLI_VERSION}"

ENV YQ_VERSION 2.4.1
RUN \
    curl -Lo "yq" "https://github.com/mikefarah/yq/releases/download/${YQ_VERSION}/yq_linux_amd64" \
    \
    && chmod +x "yq" \
    && mv "yq" "/usr/bin/yq"

ENV TERRAFORM_VERSION 0.12.18
RUN \
    curl -Lo "terraform.zip" "https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip" \
    \
    && unzip "terraform.zip" \
    && rm "terraform.zip" \
    \
    && chmod +x "terraform" \
    && mv "terraform" "/usr/bin/terraform"

ENV TERRAGRUNT_VERSION 0.21.10
RUN \
    curl -Lo "terragrunt" "https://github.com/gruntwork-io/terragrunt/releases/download/v${TERRAGRUNT_VERSION}/terragrunt_linux_amd64" \
    \
    && chmod +x "terragrunt" \
    && mv "terragrunt" "/usr/bin/terragrunt"
