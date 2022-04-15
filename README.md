## Hal docker-based build environments

This repository is the source for automated builds of standard docker images available for Hal build environments.

Hal is a release and deployment portal. See more information here: [hal-platform/hal](https://github.com/hal-platform/hal). See images on Docker Hub: [hub.docker.com/r/halplatform](https://hub.docker.com/r/halplatform/hal-build-environments)

## Should I deploy these containers?

No! All containers for designed for robust build environments. That means many dependencies required for **building and compiling** your project. Usually these dependencies are not required for **running** your project in a production-like environment.

## Available Environments

#### Windows

Windows containers have all versions of .NET Framework 4.x and .NET Core 1.x and 2.x.

> **Note:** Windows builds are not automated as no CI platform currently supports windows docker containers.
> Windows containers are limited on what versions of windows they can be used with. See
> [version-compatibility](https://docs.microsoft.com/en-us/virtualization/windowscontainers/deploy-containers/version-compatibility) for more information.

- `vs2015` ([windows/vs2015/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/windows/vs2015/Dockerfile)) (Windows Server Core 2016 - Visual Studio 2015)
- `vs2017` ([windows/vs2017/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/windows/vs2017/Dockerfile)) (Windows Server Core 2016 - Visual Studio 2017)
- `vs2015-server2019` ([windows/vs2015-server2019/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/windows/vs2015-server2019/Dockerfile)) (Windows Server Core 2019 - Visual Studio 2015)
- `vs2017-server2019` ([windows/vs2017-server2019/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/windows/vs2017-server2019/Dockerfile)) (Windows Server Core 2019 - Visual Studio 2017)

> No container contains .NET Framework 3.5.  
> See https://github.com/Microsoft/dotnet-framework-docker/blob/master/3.5/Dockerfile

#### Linux

- `debian8-buildpack` ([linux/debian8/buildpack/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/linux/debian8/buildpack/Dockerfile))
- `debian9-buildpack` ([linux/debian9/buildpack/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/linux/debian9/buildpack/Dockerfile))
- `debian10-buildpack` ([linux/debian10/buildpack/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/linux/debian10/buildpack/Dockerfile))
- `centos6-buildpack` ([linux/centos6/buildpack/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/linux/centos6/buildpack/Dockerfile)) (Centos 6.9)
- `centos7-buildpack` ([linux/centos7/buildpack/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/linux/centos7/buildpack/Dockerfile)) (Centos 7.4)

#### Tools

- `awscli1.11` ([tools/awscli/1.11/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/tools/awscli/1.11/Dockerfile))
- `awscli1.14` ([tools/awscli/1.14/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/tools/awscli/1.14/Dockerfile))
- `awscli1.16` ([tools/awscli/1.16/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/tools/awscli/1.16/Dockerfile))
- `terraform0.11` ([tools/terraform/0.11/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/tools/terraform/0.11/Dockerfile))
- `terraform0.12` ([tools/terraform/0.12/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/tools/terraform/0.12/Dockerfile))
- `docker17.06` ([tools/docker/17.06/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/tools/docker/17.06/Dockerfile))
- `docker18.03` ([tools/docker/18.03/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/tools/docker/18.03/Dockerfile))
- `docker19.03` ([tools/docker/19.03/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/tools/docker/19.03/Dockerfile))

#### Elixir

- `elixir1.2-centos7` ([elixir/1.2/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/elixir/1.2/Dockerfile)) (Erlang 18.3)
- `elixir1.3-centos7` ([elixir/1.3/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/elixir/1.3/Dockerfile)) (Erlang 19.3)
- `elixir1.4-centos7` ([elixir/1.4/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/elixir/1.4/Dockerfile)) (Erlang 19.3)
- `elixir1.5-centos7` ([elixir/1.5/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/elixir/1.5/Dockerfile)) (Erlang 20.1)
- `elixir1.6-centos7` ([elixir/1.6/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/elixir/1.6/Dockerfile)) (Erlang 20.2)

#### Node

- `node4.8-centos7` ([node/4.8/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/node/4.8/Dockerfile))
- `node6.13-centos7` ([node/6.13/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/node/6.13/Dockerfile))
- `node8.10-centos7` ([node/8.10/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/node/8.10/Dockerfile))
- `node10.10-centos7` ([node/10.10/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/node/10.10/Dockerfile))
- `node12.12-centos7` ([node/12.12/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/node/12.12/Dockerfile))

#### PHP

- `php5.6-centos7` ([php/5.6/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/php/5.6/Dockerfile))
- `php7.0-centos7` ([php/7.0/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/php/7.0/Dockerfile))
- `php7.1-centos7` ([php/7.1/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/php/7.1/Dockerfile))
- `php7.2-centos7` ([php/7.2/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/php/7.2/Dockerfile))
- `php7.3-debian9` ([php/7.3/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/php/7.3/Dockerfile))
- `php7.4-debian10` ([php/7.4/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/php/7.4/Dockerfile))

#### Dotnet Core

- `dotnet1.1-debian8` ([dotnet/1.1/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/dotnet/1.1/Dockerfile))
- `dotnet2.0-debian8` ([dotnet/2.0/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/dotnet/2.0/Dockerfile))
- `dotnet2.1-debian8` ([dotnet/2.1/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/dotnet/2.1/Dockerfile))
- `dotnet2.2-debian9` ([dotnet/2.2/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/dotnet/2.2/Dockerfile))
- `dotnet3.1-debian10` ([dotnet/3.1/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/dotnet/3.1/Dockerfile))

#### Python

- `python2.7-debian9` ([python/2.7-debian/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/python/2.7-debian/Dockerfile))
- `python2.7-centos7` ([python/2.7/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/python/2.7/Dockerfile))
- `python3.6-debian9` ([python/3.6-debian/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/python/3.6-debian/Dockerfile))
- `python3.6-centos7` ([python/3.6/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/python/3.6/Dockerfile))
