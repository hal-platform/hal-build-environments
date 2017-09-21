## Hal docker-based build environments

This repository is the source for automated builds of standard docker images available for Hal build environments.

Hal is a release and deployment platform developed by Quicken Loans. See more information here: [hal-platform/hal](https://github.com/hal-platform/hal)

Docker Hub: [hub.docker.com/r/halplatform](https://hub.docker.com/r/halplatform/hal-build-environments)

## Environments

#### Windows

Windows containers have all versions of .NET Framework 4.x and .NET core 1.x and 2.x.

> No container contains .NET Framework 3.5.
> See https://github.com/Microsoft/dotnet-framework-docker/blob/master/3.5/Dockerfile

- [Windows Server Core - Visual Studio 2015](https://github.com/hal-platform/hal-build-environments/blob/master/windows/vs2015/Dockerfile)
- [Windows Server Core - Visual Studio 2017](https://github.com/hal-platform/hal-build-environments/blob/master/windows/vs2017/Dockerfile)

#### Linux

- [Debian Jessie - Buildpack](https://github.com/hal-platform/hal-build-environments/blob/master/linux/debian8/buildpack/Dockerfile)
