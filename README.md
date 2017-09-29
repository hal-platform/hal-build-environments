## Hal docker-based build environments

This repository is the source for automated builds of standard docker images available for Hal build environments.

Hal is a release and deployment platform developed by Quicken Loans.

See more information here: [hal-platform/hal](https://github.com/hal-platform/hal)

Docker Hub: [hub.docker.com/r/halplatform](https://hub.docker.com/r/halplatform/hal-build-environments)

## Should I deploy these containers?

No! All containers for designed for robust build environments. That means many dependencies required for **building and compiling** your project. Usually these dependencies are not required for **running** your project in a production-like environment.

## Available Environments

#### Windows

Windows containers have all versions of .NET Framework 4.x and .NET core 1.x and 2.x.

- `vs2015` ([windows/vs2015/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/windows/vs2015/Dockerfile)) (Windows Server Core - Visual Studio 2015)
- `vs2017` ([windows/vs2017/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/windows/vs2017/Dockerfile)) (Windows Server Core - Visual Studio 2017)

> No container contains .NET Framework 3.5.  
> See https://github.com/Microsoft/dotnet-framework-docker/blob/master/3.5/Dockerfile

#### Linux

- `debian8-buildpack` ([linux/debian8/buildpack/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/linux/debian8/buildpack/Dockerfile))
- `centos6-buildpack` ([linux/centos6/buildpack/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/linux/centos6/buildpack/Dockerfile)) (Centos 6.9)
- `centos7-buildpack` ([linux/centos7/buildpack/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/linux/centos7/buildpack/Dockerfile)) (Centos 7.4)

#### Tools

- `awscli` ([tools/awscli/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/tools/awscli/Dockerfile))

#### Elixir

- `elixir1.2-centos7` ([elixir/1.2/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/elixir/1.2/Dockerfile)) (Erlang 18.3)
- `elixir1.3-centos7` ([elixir/1.3/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/elixir/1.3/Dockerfile)) (Erlang 19.3)
- `elixir1.4-centos7` ([elixir/1.4/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/elixir/1.4/Dockerfile)) (Erlang 19.3)
- `elixir1.5-centos7` ([elixir/1.5/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/elixir/1.5/Dockerfile)) (Erlang 20.1)

#### Node

- `node4.8-centos7` ([node/4.8/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/node/4,8/Dockerfile))
- `node6.11-centos7` ([node/6.11/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/node/6.11/Dockerfile))
- `node8.6-centos7` ([node/8.6/Dockerfile](https://github.com/hal-platform/hal-build-environments/blob/master/node/8.6/Dockerfile))
