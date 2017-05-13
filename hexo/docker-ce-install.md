---
title: Docker-CentOS下安装Docker
date: 2017-05-13
description: "CentOS下卸载与重新安装最新版本docker-ce"
categories: [Docker]
tags: [Docker]
---

### OS requirements
To install Docker, you need the 64-bit version of CentOS 7.

### Uninstall old versions
Older versions of Docker were called `docker` or `docker-engine`. If these are installed, uninstall them, along with associated dependencies.

The contents of `/var/lib/docker/`, including images, containers, volumes, and networks, should be deleted.

```shell
$ yum list installed | grep docker
$ sudo yum remove docker \
                  docker-common \
                  container-selinux \
                  docker-selinux \
                  docker-engine

$ rm -rf /var/lib/docker
```

## Install Docker
### Install using the repository
> 1. Set up the repository
Set up the Docker CE repository on CentOS:
```shell
$ sudo yum install -y yum-utils

$ sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo

$ sudo yum makecache fast
```

> 2. Get Docker CE
Install the latest version of Docker CE on CentOS:
```shell
$ sudo yum -y install docker-ce
```
Start Docker:
```shell
$ sudo systemctl start docker
```

> 3. Test your Docker CE installation
Test your installation:
```shell
$ sudo docker run hello-world
```

### Uninstall Docker
> 1. Uninstall the Docker package:

| Docker Edition  | Command             |
| ------------- |:-------------------:|
| Docker CE     | `sudo yum remove docker-ce`  |
| Docker EE     | `sudo yum remove docker-ce`  |


> 2. Images, containers, volumes, or customized configuration files on your host are not automatically removed. To delete all images, containers, and volumes:
```shell
$ sudo rm -rf /var/lib/docker
```
You must delete any edited configuration files manually.