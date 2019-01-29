FROM microsoft/dotnet-framework:4.7.2-sdk-windowsservercore-ltsc2019
# See https://github.com/Microsoft/dotnet-framework-docker/blob/33531c3bae718f970b704730703ba1fb0f3dff80/4.7.2/sdk/windowsservercore-ltsc2019/Dockerfile

# Container Compatibility
# See https://docs.microsoft.com/en-us/virtualization/windowscontainers/deploy-containers/version-compatibility

# We use a similar configuration as Microsoft's VSTS agents (this is deprecated)
# https://github.com/Microsoft/vsts-agent-docker/blob/master/windows/servercore/10.0.14393/standard/VS2017/Dockerfile

RUN Install-PackageProvider -Name chocolatey -RequiredVersion 2.8.5.130 -Force
ENV chocolateyUseWindowsCompression=false
RUN [Environment]::SetEnvironmentVariable('PATH', $Env:path+';'+$Env:ChocolateyInstall + '\bin;');
RUN choco config set cachelocation C:\chococache

RUN Install-Package git -Force
RUN Install-Package nodejs -Force
RUN Install-Package jdk8 -Force
RUN Install-Package curl -Force
RUN Install-Package maven -Force
RUN Install-Package gradle -Force
RUN Install-Package docker -Force

# NOTE: This step takes FOREVER. Be prepared to wait 4+ hours.
RUN choco install \
    visualstudio2015enterprise \
    --package-parameters "--passive --locale en-US --includeOptional" \
    --confirm \
    --limit-output \
    --timeout 81600 \
    \
    && rmdir /S /Q C:\chococache

# Install NuGet, .NET Framework 4.5, 4.6, 4.7

RUN Install-Package nuget.commandline -Force
RUN Install-Package netfx-4.0.3-devpack -Force
RUN Install-Package netfx-4.5.2-devpack -Force
RUN Install-Package netfx-4.6.2-devpack -Force
RUN Install-Package netfx-4.7.2-devpack -Force

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

RUN [Environment]::SetEnvironmentVariable('PATH', $Env:path+';'+$Env:ProgramFiles(x86) + '\MSBuild\14.0\Bin;');
RUN [Environment]::SetEnvironmentVariable('PATH', $Env:path+';'+$Env:ProgramFiles(x86) + '\Microsoft Visual Studio 14.0\Common7\IDE;');
RUN [Environment]::SetEnvironmentVariable('PATH', $Env:path+';'+$Env:ProgramFiles(x86) + '\Microsoft Visual Studio 14.0\Common7\IDE\CommonExtensions\Microsoft\TestWindow;');
RUN [Environment]::SetEnvironmentVariable('PATH', $Env:path+';'+$Env:ProgramFiles(x86) + '\dotnet;');

# Trigger the population of the local package cache
ENV NUGET_XMLDOC_MODE skip

RUN mkdir C:\warmup \
    && cd C:\warmup \
    && dotnet new \
    && cd .. \
    && rmdir /S /Q C:\warmup
