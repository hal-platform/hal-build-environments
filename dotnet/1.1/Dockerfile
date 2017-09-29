FROM halplatform/hal-build-environments:debian8-buildpack

# Install .NET CLI dependencies
RUN \
    apt-get update \
        && \
    apt-get install -y --no-install-recommends \
        libc6 \
        libcurl3 \
        libgcc1 \
        libgssapi-krb5-2 \
        libicu52 \
        liblttng-ust0 \
        libssl1.0.0 \
        libstdc++6 \
        libunwind8 \
        libuuid1 \
        zlib1g \
        && \
    rm -rf /var/lib/apt/lists/*

# Install .NET Core SDK
ENV DOTNET_SDK_VERSION      "1.1.4"
ENV DOTNET_SDK_DOWNLOAD_URL "https://dotnetcli.blob.core.windows.net/dotnet/Sdk/${DOTNET_SDK_VERSION}/dotnet-dev-debian-x64.${DOTNET_SDK_VERSION}.tar.gz"
ENV DOTNET_SDK_DOWNLOAD_SHA "8fc1b1dd5fe84a9ecc91acc5a20b3bb22489655f63567848ec3eba7daa497b9e4c3cbe54669164853e3f917a7822ff2e607e396aff96d3e81bf30620683f7f59"

RUN curl -SL "${DOTNET_SDK_DOWNLOAD_URL}" --output dotnet.tar.gz \
        && \
    echo "${DOTNET_SDK_DOWNLOAD_SHA} dotnet.tar.gz" | sha512sum -c - \
        && \
    mkdir -p /usr/share/dotnet \
        && \
    tar -zxf dotnet.tar.gz -C /usr/share/dotnet \
        && \
    rm dotnet.tar.gz \
        && \
    ln -s /usr/share/dotnet/dotnet /usr/bin/dotnet

# Trigger the population of the local package cache
ENV NUGET_XMLDOC_MODE skip
RUN mkdir warmup \
        && \
    cd warmup \
        && \
    dotnet new \
        && \
    cd .. \
        && \
    rm -rf warmup \
        && \
    rm -rf /tmp/NuGetScratch
