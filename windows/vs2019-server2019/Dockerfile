# Because its impossible to search for microsoft images anymore:
# https://hub.docker.com/_/microsoft-dotnet-framework-sdk
FROM mcr.microsoft.com/dotnet/framework/sdk:4.8-windowsservercore-ltsc2019

# https://github.com/microsoft/dotnet-framework-docker/blob/7ea28f0c8e/4.8/sdk/windowsservercore-ltsc2019/Dockerfile

# Container Compatibility
# See https://docs.microsoft.com/en-us/virtualization/windowscontainers/deploy-containers/version-compatibility

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

ENV chocolateyUseWindowsCompression=false
RUN iex (wget 'https://chocolatey.org/install.ps1' -UseBasicParsing)

RUN choco feature enable -n=allowGlobalConfirmation
RUN choco feature disable -n=showDownloadProgress
RUN choco config set cachelocation "/chococache"

RUN choco install \
    git  \
    nodejs \
    jdk8 \
    curl \
    maven \
    gradle \
    docker-cli \
    --limit-output \
    --timeout 3600 \
    ; Remove-Item "/chococache"  -Recurse -Force

# Package parameters is BROKEN
# --package-parameters '--passive --includeOptional --locale en-US' \
RUN choco install \
    visualstudio2019enterprise \
    --limit-output \
    --timeout 3600 \
    ; Remove-Item "/chococache"  -Recurse -Force

# Already installed in base image:
# - NuGet
# - visualstudio2019-workload-netcoretools
# - Microsoft.Net.Component.4.8.SDK
# - Microsoft.VisualStudio.Workload.MSBuildTools
RUN choco install \
    visualstudio2019-workload-netweb \
    visualstudio2019-workload-webbuildtools \
    --limit-output \
    --timeout 3600 \
    --ignore-package-exit-codes \
    --package-parameters "--includeOptional" \
    ; Remove-Item "/chococache"  -Recurse -Force

# Install .NET Framework 4.5, 4.6, 4.7, 4.8
RUN choco install \
    netfx-4.8-devpack \
    netfx-4.7.2-devpack \
    netfx-4.6.2-devpack \
    netfx-4.5.2-devpack \
    --limit-output \
    --timeout 1800 \
    --ignore-package-exit-codes \
    ; Remove-Item "/chococache"  -Recurse -Force

# Install .NET Core 2.1
RUN Invoke-WebRequest \
    "https://dotnetcli.azureedge.net/dotnet/Sdk/2.1.806/dotnet-sdk-2.1.806-win-x64.zip" \
    -OutFile dotnet.zip; \
    Expand-Archive dotnet.zip \
        -DestinationPath "${Env:ProgramFiles}\dotnet" \
        -Force; \
    Remove-Item -Force dotnet.zip

# Install .NET Core 3.1
RUN Invoke-WebRequest \
    "https://dotnetcli.azureedge.net/dotnet/Sdk/3.1.202/dotnet-sdk-3.1.202-win-x64.zip" \
    -OutFile dotnet.zip; \
    Expand-Archive dotnet.zip \
        -DestinationPath "${Env:ProgramFiles}\dotnet" \
        -Force; \
    Remove-Item -Force dotnet.zip

# In order to set system PATH, ContainerAdministrator must be used
USER ContainerAdministrator
RUN setx /M PATH "%PATH%;C:\Program Files\dotnet"
USER ContainerUser

# Trigger the population of the local package cache
ENV NUGET_XMLDOC_MODE skip
ENV DOTNET_CLI_TELEMETRY_OPTOUT 1

RUN dotnet --list-sdks ; \
    mkdir C:\warmup ; \
    cd C:\warmup ; \
    dotnet new ; \
    cd .. ; \
    Remove-Item C:\warmup -Force -Recurse
