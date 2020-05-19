# Because its impossible to search for microsoft images anymore:
# https://hub.docker.com/_/microsoft-dotnet-framework-sdk
# NOTE: DO NOT use "mcr.microsoft.com/dotnet/framework/sdk:4.8-windowsservercore-ltsc2019" as it uses vs2019
FROM mcr.microsoft.com/dotnet/framework/runtime:4.8-windowsservercore-ltsc2019

# https://github.com/microsoft/dotnet-framework-docker/blob/7ea28f0c8e9ca278eb5d38c67fe67987e8432ed8/4.8/sdk/windowsservercore-1903/Dockerfile
# See https://github.com/Microsoft/dotnet-framework-docker/blob/33531c3bae718f970b704730703ba1fb0f3dff80/4.7.2/sdk/windowsservercore-ltsc2019/Dockerfile

# Container Compatibility
# See https://docs.microsoft.com/en-us/virtualization/windowscontainers/deploy-containers/version-compatibility

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

ENV chocolateyUseWindowsCompression=false
RUN iex (wget 'https://chocolatey.org/install.ps1' -UseBasicParsing)

# Download the Build Tools bootstrapper.
ADD "https://aka.ms/vs/15/release/vs_buildtools.exe" "C:\TEMP\vs_buildtools.exe"

SHELL ["cmd", "/S", "/C"]

# Installer won't detect DOTNET_SKIP_FIRST_TIME_EXPERIENCE if ENV is used, must use setx /M
# Install VS components
RUN setx /M DOTNET_SKIP_FIRST_TIME_EXPERIENCE 1 \
    && start /w C:\TEMP\vs_BuildTools.exe ^ \
        --add Microsoft.VisualStudio.Workload.MSBuildTools ^ \
        --add Microsoft.VisualStudio.Workload.NetCoreBuildTools ^ \
        --add Microsoft.Component.ClickOnce.MSBuild ^ \
        --add Microsoft.VisualStudio.Component.WebDeploy ^ \
        --quiet --norestart --nocache --wait \
    && powershell -Command "if ($err = dir $Env:TEMP -Filter dd_setup_*_errors.log | where Length -gt 0 | Get-Content) { throw $err }" \
    && del C:\TEMP\vs_BuildTools.exe \
    \
    # Cleanup
    && rmdir /S /Q "%ProgramFiles(x86)%\Microsoft Visual Studio\Installer" \
    && powershell Remove-Item -Force -Recurse "%TEMP%\*" \
    && rmdir /S /Q "%ProgramData%\Package Cache"

# Install web targets
RUN curl -fSLo MSBuild.Microsoft.VisualStudio.Web.targets.zip https://dotnetbinaries.blob.core.windows.net/dockerassets/MSBuild.Microsoft.VisualStudio.Web.targets.2020.03.zip \
    && tar -zxf MSBuild.Microsoft.VisualStudio.Web.targets.zip -C "%ProgramFiles(x86)%\Microsoft Visual Studio\2017\BuildTools\MSBuild\Microsoft\VisualStudio\v15.0" \
    && del MSBuild.Microsoft.VisualStudio.Web.targets.zip

RUN choco feature enable -n=allowGlobalConfirmation
RUN choco feature disable -n=showDownloadProgress
RUN choco config set cachelocation C:\chococache

RUN choco install \
    git  \
    nodejs \
    jdk8 \
    curl \
    maven \
    gradle \
    docker \
    --limit-output \
    --timeout 3600 \
    ; Remove-Item C:\chococache  -Recurse -Force

RUN choco install \
    visualstudio2017enterprise \
    --package-parameters "--passive --locale en-US --includeOptional" \
    --limit-output \
    --timeout 3600 \
    ; Remove-Item C:\chococache  -Recurse -Force

RUN choco install \
    visualstudio2017-workload-netcoretools \
    visualstudio2017-workload-netweb \
    --limit-output \
    --timeout 3600 \
    --ignore-package-exit-codes \
    --package-parameters "--includeOptional" \
    ; Remove-Item C:\chococache  -Recurse -Force

# Install NuGet, .NET Framework 4.5, 4.6, 4.7
RUN choco install \
    nuget.commandline \
    netfx-4.7.2-devpack \
    netfx-4.6.2-devpack \
    netfx-4.5.2-devpack \
    --limit-output \
    --timeout 1800 \
    --ignore-package-exit-codes \
    ; Remove-Item C:\chococache  -Recurse -Force

# Targeting Packs
RUN "@('4.0', '4.5.2', '4.6.2', '4.7.2', '4.8') | %{ \
        Invoke-WebRequest \
            -UseBasicParsing \
            -Uri https://dotnetbinaries.blob.core.windows.net/referenceassemblies/v${_}.zip \
            -OutFile referenceassemblies.zip; \
        Expand-Archive referenceassemblies.zip \
            -DestinationPath \"${Env:ProgramFiles(x86)}\Reference Assemblies\Microsoft\Framework\.NETFramework\" \
            -Force; \
        Remove-Item -Force referenceassemblies.zip; \
    }"

# Install .NET Core 2.0
ENV DOTNET_DOWNLOAD_URL     https://download.microsoft.com/download/5/F/0/5F0362BD-7D0A-4A9D-9BF9-022C6B15B04D/dotnet-runtime-2.0.0-win-x64.zip
ENV DOTNET_SDK_DOWNLOAD_URL https://download.microsoft.com/download/1/B/4/1B4DE605-8378-47A5-B01B-2C79D6C55519/dotnet-sdk-2.0.0-win-x64.zip

RUN Invoke-WebRequest $Env:DOTNET_DOWNLOAD_URL -OutFile dotnet.zip; \
    Expand-Archive dotnet.zip -DestinationPath $Env:ProgramFiles\dotnet -Force; \
    Remove-Item -Force dotnet.zip

RUN Invoke-WebRequest $Env:DOTNET_SDK_DOWNLOAD_URL -OutFile dotnet.zip; \
    Expand-Archive dotnet.zip -DestinationPath $Env:ProgramFiles\dotnet -Force; \
    Remove-Item -Force dotnet.zip

# Install .NET Core 2.2
ENV DOTNET_DOWNLOAD_URL https://download.visualstudio.microsoft.com/download/pr/c332d70f-6582-4471-96af-4b0c17a616ad/5f3043d4bc506bf91cb89fa90462bb58/dotnet-sdk-2.2.103-win-x64.zip

RUN Invoke-WebRequest $Env:DOTNET_DOWNLOAD_URL -OutFile dotnet.zip; \
    Expand-Archive dotnet.zip -DestinationPath $Env:ProgramFiles\dotnet -Force; \
    Remove-Item -Force dotnet.zip

SHELL ["cmd", "/S", "/C"]

# Set PATH in one layer to keep image size down.
RUN powershell setx /M PATH $(${Env:PATH} \
    + \";${Env:ProgramFiles}\NuGet\" \
    + \";${Env:ProgramFiles(x86)}\MSBuild\15.0\Bin\" \
    + \";${Env:ProgramFiles(x86)}\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\" \
    + \";${Env:ProgramFiles(x86)}\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\CommonExtensions\Microsoft\TestWindow\" \
    + \";${Env:ProgramFiles(x86)}\Microsoft SDKs\Windows\v10.0A\bin\NETFX 4.8 Tools\" \
    + \";${Env:ProgramFiles(x86)}\Microsoft SDKs\ClickOnce\SignTool\")

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

# Trigger the population of the local package cache
ENV NUGET_XMLDOC_MODE skip
ENV DOTNET_CLI_TELEMETRY_OPTOUT 1

RUN dotnet --list-sdks ; \
    mkdir C:\warmup ; \
    cd C:\warmup ; \
    dotnet new ; \
    cd .. ; \
    Remove-Item C:\warmup -Force -Recurse
