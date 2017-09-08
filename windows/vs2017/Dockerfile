FROM microsoft/windowsservercore:10.0.14393.1480

# We use the same configuration as microsoft's VSTS agents
# https://github.com/Microsoft/vsts-agent-docker/blob/master/windows/servercore/10.0.14393/standard/VS2017/Dockerfile
# todo add dotnet 3.5
# - see https://github.com/MicrosoftDocs/Virtualization-Documentation/blob/master/windows-container-samples/dotnet35/Dockerfile

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
    ant \
    docker \
    ruby \
    --confirm \
    --limit-output \
    --timeout 3600 \
    && rmdir /S /Q C:\chococache
   # choco install visualstudio2015community --confirm --timeout 216000 \

RUN choco install \
    dotnet4.6.1 \
    --confirm \
    --limit-output \
    && rmdir /S /Q C:\chococache

RUN choco install \
    visualstudio2017enterprise \
    --package-parameters "--passive --locale en-US --includeOptional" \
    --confirm \
    --limit-output \
    --timeout 3600 \
    && rmdir /S /Q C:\chococache

RUN choco install \
    visualstudio2017-workload-netcoretools \
    visualstudio2017-workload-netweb \
    --confirm \
    --limit-output \
    --timeout 3600 \
    --ignore-package-exit-codes \
    --package-parameters "--includeOptional" \
    && rmdir /S /Q C:\chococache

# common node tools
RUN npm install gulp -g && npm install grunt -g && npm install -g less && npm install phantomjs-prebuilt -g

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

SHELL ["cmd", "/S", "/C"]

RUN setx /M PATH "%PATH%;%ProgramFiles%\dotnet"

# Trigger the population of the local package cache
ENV NUGET_XMLDOC_MODE skip

RUN mkdir C:\warmup \
    && cd C:\warmup \
    && dotnet new \
    && cd .. \
    && rmdir /S /Q C:\warmup
