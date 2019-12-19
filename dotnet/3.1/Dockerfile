FROM halplatform/hal-build-environments:debian10-buildpack

# Install .NET CLI dependencies
RUN \
    apt-get update \
        && \
    apt-get install -y --no-install-recommends \
        libicu63 \
        libssl1.1 \
        libc6 \
        libgcc1 \
        libgssapi-krb5-2 \
        liblttng-ust0 \
        libstdc++6 \
        zlib1g \
        \
        gettext \
        apt-transport-https \
        && \
    rm -rf /var/lib/apt/lists/*

ENV DOTNET_SDK_VERSION "3.1"
ENV DOTNET_PACKAGE_VERSION "3.1.100"
ENV POWERSHELL_VERSION "7.0.0-rc.1"

# Install Dotnet

RUN curl -sL "https://packages.microsoft.com/keys/microsoft.asc" | apt-key add - \
        && \
    curl -sLo "/etc/apt/sources.list.d/microsoft.list" \
        "https://packages.microsoft.com/config/debian/10/prod.list" \
        && \
    apt-get update \
        && \
    apt-get install -y \
        "dotnet-sdk-${DOTNET_SDK_VERSION}=${DOTNET_PACKAGE_VERSION}-1" \
        && \
    rm -rf /var/lib/apt/lists/*

# Install Powershell

RUN curl -sLo "/tmp/powershell.tgz" \
    "https://github.com/PowerShell/PowerShell/releases/download/v${POWERSHELL_VERSION}/powershell-${POWERSHELL_VERSION}-linux-x64.tar.gz" \
        && \
    mkdir -p "/opt/microsoft/powershell/7" \
        && \
    tar zxf "/tmp/powershell.tgz" -C "/opt/microsoft/powershell/7" \
        && \
    chmod +x "/opt/microsoft/powershell/7/pwsh" \
        && \
    ln -s "/opt/microsoft/powershell/7/pwsh" /usr/bin/pwsh

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
