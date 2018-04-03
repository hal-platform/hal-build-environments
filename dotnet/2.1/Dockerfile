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
        \
        libunwind8 \
        gettext \
        apt-transport-https \
        && \
    rm -rf /var/lib/apt/lists/*

ENV DOTNET_SDK_VERSION "2.1.101"
ENV POWERSHELL_VERSION "6.0.2"

RUN curl "https://packages.microsoft.com/keys/microsoft.asc" | apt-key add - \
        && \
    echo 'deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-jessie-prod jessie main' > "/etc/apt/sources.list.d/microsoft.list" \
        && \
    apt-get update \
        && \
apt-cache madison powershell && \
    apt-get install -y --no-install-recommends \
        "dotnet-sdk-${DOTNET_SDK_VERSION}" \
        "powershell=${POWERSHELL_VERSION}-1.debian.8" \
        && \
    rm -rf /var/lib/apt/lists/*

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
