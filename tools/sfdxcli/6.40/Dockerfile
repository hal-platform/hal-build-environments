FROM halplatform/hal-build-environments:node10.10-debian9

ENV SFDX_VERSION "6.40.0"
ENV SFDX_HASH "384e0c6cf2"

# RUN yarn global add sfdx-cli@"${SFDX_VERSION}"
RUN curl -L -o sfdx.tar.xz https://developer.salesforce.com/media/salesforce-cli/sfdx-cli/channels/stable/sfdx-cli-v"${SFDX_VERSION}"-"${SFDX_HASH}"-linux-x64.tar.xz \
        && \
    echo "c0582b0c2b07b0a1ebdbc9e022a24fad5a75c0e3bee8122c3f2fce60b9daf3a0 *sfdx.tar.xz" | sha256sum --check \
        && \
    mkdir -p sfdx \
        && \
    tar xJf sfdx.tar.xz -C sfdx --strip-components 1 \
        && \
    ./sfdx/install \
        && \
    rm -rf sfdx sfdx.tar.xz
