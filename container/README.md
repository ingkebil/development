# Containers ^*

1. [Introduction](#1-introduction)
2. [Singularity](#1-singularity)
	1. [Install](#21-install)
	1. [Download an image](#22-download)
	1. [Build an image](#23-build)
	1. [Interact with an image](#24-interact)
3. [Docker](#2-docker) 

\* This document will focus on two platforms: [Docker] and [Singularity].

## 1. Introduction

In the Docker-world, "A Container is defined as an instance of an image. \[Which in turn\] An image is an snapshot of a container" ^[1] . And it is more or less the same in the Singularity-world ^[2] . In other words, a user can launch a container from an image ^[3] .

Singularity and Docker platforms provide functionality of virtualization without emphasis of emulation and host OS. In bioinformatic data analysis, much like any other data sciences, these platforms provide containers for packaging of the softwares and their dependencies. These containers can even hold the data required for the specific bioinformatic workflow within the container's environment. This makes it feasible to seamlessly create data analysis environments for reproducibility, mobility, compatibility, and security ^[2] .

## 2. Singularity

For complete guide on Singularity please refer to: [http://singularity.lbl.gov/quickstart](http://singularity.lbl.gov/quickstart) .

### 2.1 Install

For installation on Linux please follow the guide on: [http://singularity.lbl.gov/install-linux](http://singularity.lbl.gov/install-linux). And for Mac OS X installation it can be installed via Vagrant: [http://singularity.lbl.gov/install-mac](http://singularity.lbl.gov/install-mac)

### 2.2 Download an image

There are two commands to download pre-built Singularity image: ```pull``` and ```build```. ```Pull``` is basically similar to cloning a repositories. 
### 2.3 Build an image

### 2.4 Interact with an image

## 3. Docker

TBA


[Docker]: https://www.docker.com/
[Singularity]: http://singularity.lbl.gov/
[1]: http://paislee.io/how-to-automate-docker-deployments/
[2]: http://singularity.lbl.gov/
[3]: https://docs.docker.com/get-started/
