[![ci](https://github.com/lord-of-dock/docker-net-tools/actions/workflows/ci.yml/badge.svg)](https://github.com/lord-of-dock/docker-net-tools/actions/workflows/ci.yml)

[![GitHub license](https://img.shields.io/github/license/lord-of-dock/docker-net-tools)](https://github.com/lord-of-dock/docker-net-tools)
[![GitHub latest SemVer tag)](https://img.shields.io/github/v/tag/lord-of-dock/docker-net-tools)](https://github.com/lord-of-dock/docker-net-tools/tags)
[![GitHub release)](https://img.shields.io/github/v/release/lord-of-dock/docker-net-tools)](https://github.com/lord-of-dock/docker-net-tools/releases)

[![docker version semver](https://img.shields.io/docker/v/sinlov/docker-net-tools?sort=semver)](https://hub.docker.com/r/sinlov/docker-net-tools)
[![docker image size](https://img.shields.io/docker/image-size/sinlov/docker-net-tools)](https://hub.docker.com/r/sinlov/docker-net-tools)
[![docker pulls](https://img.shields.io/docker/pulls/sinlov/docker-net-tools)](https://hub.docker.com/r/sinlov/docker-net-tools/tags?page=1&ordering=last_updated)

# docker-net-tools

- docker hub see [https://hub.docker.com/r/sinlov/docker-net-tools](https://hub.docker.com/r/sinlov/docker-net-tools)

## for

- simple image with network troubleshooting utils

```bash
## tmux
# create new session
tmux new -t net-tools
# attach to session
tmux at -t net-tools

## nc
nc -zv [ip] [port]
nc -zuv [ip] [port]
## ping
ping -c 3 [ip]
## curl
curl -v https://httpbin.org/status/200
## iperf3
# server
iperf3 -s
iperf3 -s --port 59980
# client
iperf3 -p 5201 -c [server ip]
iperf3 -p 5201 -c [server ip] -R
```

### alpine

install kits:

```bash
bash bind-tools curl jq nmap net-tools iperf3 tmux busybox-extras
```

- use telnet as:

```
busybox-extras telnet localhost 6900
```

### fast use

```bash
# use as tty
docker run --rm -it \
  --entrypoint /bin/bash \
  --name "test-docker-net-tools" \
  sinlov/docker-net-tools:latest

# see versions
docker run --rm \
  sinlov/docker-net-tools:latest \
  bash -c ' \
  uname -asrm && \
  cat /etc/os-release && \
  jq --version && \
  curl --version && \
  nmap --version && \
  bash --version '
```

## source repo

[https://github.com/lord-of-dock/docker-net-tools](https://github.com/lord-of-dock/docker-net-tools)

## source usage

### env

- parent image `alpine` version `3.20.3`

### todo-list

- rename `lord-of-dock/docker-net-tools` to new github url
- rename docker hub user `sinlov` to new org or user
- rename docker hub `docker-net-tools` to new docker image name
- rename docker repo name at `docker-bake.hcl`
    - `docker-net-tools` to new docker image name
    - `image-basic-all` to change `platforms`
    - `image-alpine-all` to change `platforms`

- use github action for this workflow push to docker hub, must add
    - variables `ENV_DOCKERHUB_OWNER` user of docker hub
    - variables `ENV_DOCKERHUB_REPO_NAME` repo name of docker hub
    - secrets `DOCKERHUB_TOKEN` token of docker hub user from [hub.docker](https://hub.docker.com/settings/security)

- change `DOCKER_IMAGE_PLATFORMS: linux/amd64,linux/arm64/v8` to your need [docker buildx](https://docs.docker.com/buildx/working-with-buildx/)
  - also change `jobs.docker-image-buildx.strategy.matrix.docker_image.[platform]` same as `DOCKER_IMAGE_PLATFORMS`
- change `push_remote_flag: ${{ github.event.pull_request.merged == true }}` to let latest tag push to docker hub


### dev mode

```bash
# see help
$ make help
# see or check build env
$ make env

# fast build
$ make all
# clean build
$ make clean

# check env
$ make dockerEnv

# change build.dockerfile
# then test image
$ make dockerTestRestartLatest
# remove build image
$ make clean
```

then change github workflows config to use

## Contributing

[![Contributor Covenant](https://img.shields.io/badge/contributor%20covenant-v1.4-ff69b4.svg)](.github/CONTRIBUTING_DOC/CODE_OF_CONDUCT.md)
[![GitHub contributors](https://img.shields.io/github/contributors/lord-of-dock/docker-net-tools)](https://github.com/lord-of-dock/docker-net-tools/graphs/contributors)

We welcome community contributions to this project.

Please read [Contributor Guide](.github/CONTRIBUTING_DOC/CONTRIBUTING.md) for more information on how to get started.

请阅读有关 [贡献者指南](.github/CONTRIBUTING_DOC/zh-CN/CONTRIBUTING.md) 以获取更多如何入门的信息