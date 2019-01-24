FROM mcr.microsoft.com/windows/servercore:ltsc2019

# We use the same configuration as Microsoft's VSTS agents
# https://github.com/Microsoft/vsts-agent-docker/blob/master/windows/servercore/10.0.14393/standard/VS2017/Dockerfile

ENV chocolateyUseWindowsCompression=false
RUN @powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"

RUN choco config set cachelocation C:\chococache

RUN choco install \
    git  \
    nodejs \
    jdk8 \
    curl \
    maven \
    gradle \
    docker \
    --confirm \
    --limit-output \
    --timeout 3600 \
    \
    && rmdir /S /Q C:\chococache

# NOTE: This step takes FOREVER. Be prepared to wait 4+ hours.
RUN choco install \
    visualstudio2015enterprise \
    --package-parameters "--passive --locale en-US --includeOptional" \
    --confirm \
    --limit-output \
    --timeout 81600 \
    \
    && rmdir /S /Q C:\chococache

# Common node tools
RUN npm install gulp -g && \
    npm install grunt -g && \
    npm install -g less && \
    npm install phantomjs-prebuilt -g

# Install NuGet, .NET Framework 4.5, 4.6, 4.7
RUN choco install \
    nuget.commandline \
    netfx-4.7.2-devpack \
    netfx-4.6.2-devpack \
    netfx-4.5.2-devpack \
    netfx-4.0.3-devpack \
    --confirm \
    --limit-output \
    --timeout 1800 \
    --ignore-package-exit-codes \
    \
    && rmdir /S /Q C:\chococache

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

# Install .NET Core 1.0.5, 1.1.2
ENV DOTNET_DOWNLOAD_URL     https://download.microsoft.com/download/D/7/A/D7A9E4E9-5D25-4F0C-B071-210CB8267943/dotnet-win-x64.1.1.2.zip
ENV DOTNET_SDK_DOWNLOAD_URL https://download.microsoft.com/download/E/7/8/E782433E-7737-4E6C-BFBF-290A0A81C3D7/dotnet-dev-win-x64.1.0.4.zip

RUN Invoke-WebRequest $Env:DOTNET_DOWNLOAD_URL -OutFile dotnet.zip; \
    Expand-Archive dotnet.zip -DestinationPath $Env:ProgramFiles\dotnet -Force; \
    Remove-Item -Force dotnet.zip

RUN Invoke-WebRequest $Env:DOTNET_SDK_DOWNLOAD_URL -OutFile dotnet.zip; \
    Expand-Archive dotnet.zip -DestinationPath $Env:ProgramFiles\dotnet -Force; \
    Remove-Item -Force dotnet.zip

# Install .NET Core 2.0
ENV DOTNET_DOWNLOAD_URL     https://download.microsoft.com/download/5/F/0/5F0362BD-7D0A-4A9D-9BF9-022C6B15B04D/dotnet-runtime-2.0.0-win-x64.zip
ENV DOTNET_SDK_DOWNLOAD_URL https://download.microsoft.com/download/1/B/4/1B4DE605-8378-47A5-B01B-2C79D6C55519/dotnet-sdk-2.0.0-win-x64.zip

RUN Invoke-WebRequest $Env:DOTNET_DOWNLOAD_URL -OutFile dotnet.zip; \
    Expand-Archive dotnet.zip -DestinationPath $Env:ProgramFiles\dotnet -Force; \
    Remove-Item -Force dotnet.zip

RUN Invoke-WebRequest $Env:DOTNET_SDK_DOWNLOAD_URL -OutFile dotnet.zip; \
    Expand-Archive dotnet.zip -DestinationPath $Env:ProgramFiles\dotnet -Force; \
    Remove-Item -Force dotnet.zip

# Add Visual Studio tools and dotnet to PATH
SHELL ["cmd", "/S", "/C"]

RUN setx /M PATH "%PATH%;%ProgramFiles(X86)%\MSBuild\14.0\Bin"
RUN setx /M PATH "%PATH%;%ProgramFiles(X86)%\Microsoft Visual Studio 14.0\Common7\IDE"
RUN setx /M PATH "%PATH%;%ProgramFiles(X86)%\Microsoft Visual Studio 14.0\Common7\IDE\CommonExtensions\Microsoft\TestWindow"
RUN setx /M PATH "%PATH%;%ProgramFiles%\dotnet"

# Trigger the population of the local package cache
ENV NUGET_XMLDOC_MODE skip

RUN mkdir C:\warmup \
    && cd C:\warmup \
    && dotnet new \
    && cd .. \
    && rmdir /S /Q C:\warmup
