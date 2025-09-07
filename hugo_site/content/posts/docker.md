---
date: '2025-09-07T18:49:13+08:00'
title: 'Docker for Development and Testing'
draft: false
tags: ["docker", "development", "testing"]
showToc: true
TocOpen: false
hidemeta: false
comments: false
description: ""
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
---

Docker is a virtualisation tool. 
It can create lightweight, fast, isolated, and reproducible environments like virtual machines, in which an application can be tested reliably.

An docker image is a snapshot of a operating system. 
A container is a instance of an image, behaving like a running virtual machine.

## Testing Process

Say I want to test a rust project. 
With file structure like
```
.
├── Cargo.lock
├── Cargo.toml
├── src
│   └── main.rs
└── target
    ├── CACHEDIR.TAG
    └── debug
```

In a brand new machine, everything needed to test this project is the rust-cargo suite, besides the source code.
So I want the container to have them.

All containers must be built from an image. 
Custom images can be built from a `Dockerfile`. 
The dockerfile for our purpose is 

```Dockerfile 
# Dockerfile
FROM rust:1.86   # we build our image from the official rust image available on docker hub

WORKDIR /app   # set working directory to /app

COPY . .  # copy all files in current directory to /app in the container
````

To build the image, run 

```bash
docker build -t <image_name> .
docker images # list all images. You may see several images, as we have pulled one from Docker Hub
```

To instantiate a container, run 

```bash 
docker run -it <image_name> /bin/bash # file the containter interactively in command mode
```

Now use the exposed terminal to test the project.


## Docker Hub and other Registries for container

To test rust, we build our custom image from the official rust image on [Docker Hub](https://hub.docker.com/_/rust). 
There are plethora of images on Docker Hub for testing other applications, including python, nodejs, golang, debian, ubuntu, nginx, postgres, etc.

Many other image registries exist, for example, there are `gcr.io`, `quay.io`, etc.

To pull those image, simple use their url in `Dockerfile`, eg.

```Dockerfile
from quay.io/capk/ubuntu-2404-container-disk:v1.32.1
```

Images can also be pulled onto your local machine independently of a `Dockerfile`

```bash
docker pull quay.io/capk/ubuntu-2404-container-disk:v1.32.1
```

Image pulled this way have a very long name. Tag them for convenience..

```bash
docker tag quay.io/capk/ubuntu-2404-container-disk:v1.32.1 my_ubuntu:latest
```

And now the `Dockerfile` can be written as 

```Dockerfile
FROM my_ubuntu:latest
```

## In China

Docker Hub is blocked in China. 
Instead, search images on [aityp](https://docker.aityp.com/).
For example `swr.cn-north-4.myhuaweicloud.com/ddn-k8s/quay.io/capk/ubuntu-2404-container-disk:v1.32.1` is the chinese mirror of `quay.io/capk/ubuntu-2404-container-disk:v1.32.1`.

## Dockerfile for Automation

Dockerfile is extremely powerful. 
It can be used to automate the testing process.
