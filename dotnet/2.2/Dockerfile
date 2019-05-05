FROM halplatform/hal-build-environments:debian9-buildpack

# Install .NET CLI dependencies
RUN \
    apt-get update \
        && \
    apt-get install -y --no-install-recommends \
        libc6 \
        libcurl3 \
        libgcc1 \
        libgssapi-krb5-2 \
        libicu57 \
        liblttng-ust0 \
        libstdc++6 \
        zlib1g \
        \
        gettext \
        apt-transport-https \
        && \
    rm -rf /var/lib/apt/lists/*

ENV DOTNET_SDK_VERSION "2.2"
ENV DOTNET_PACKAGE_VERSION "2.2.105"
ENV POWERSHELL_VERSION "6.1.3"

RUN curl "https://packages.microsoft.com/keys/microsoft.asc" | apt-key add - \
        && \
    echo 'deb [arch=amd64] https://packages.microsoft.com/debian/9/prod stretch main' > "/etc/apt/sources.list.d/microsoft.list" \
        && \
    apt-get update \
        && \
apt-cache madison "powershell" && \
apt-cache madison "dotnet-host" && \
apt-cache madison "dotnet-sdk-${DOTNET_SDK_VERSION}" && \
    apt-get install -y \
        "dotnet-sdk-${DOTNET_SDK_VERSION}=${DOTNET_PACKAGE_VERSION}-1" \
        "dotnet-host=${DOTNET_SDK_VERSION}.4" \
        "powershell=${POWERSHELL_VERSION}-1.debian.9" \
        "aspnetcore-runtime-${DOTNET_SDK_VERSION}" \
        "dotnet-runtime-${DOTNET_SDK_VERSION}" \
        "dotnet-hostfxr-${DOTNET_SDK_VERSION}" \
        && \
    rm -rf /var/lib/apt/lists/*

ENV NUGET_XMLDOC_MODE skip
ENV DOTNET_CLI_TELEMETRY_OPTOUT 1

# Trigger the population of the local package cache
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
