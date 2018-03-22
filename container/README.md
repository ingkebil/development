# Containers *

1. [Introduction](#1-introduction)
2. [Singularity](#1-singularity)
	1. [Install](#21-install)
	1. [Download an image](#22-download)
	1. [Build an image from scratch](#23-build)
	1. [Interact with an image](#24-interact)
3. [Docker](#2-docker) 

\* This document will focus on two platforms: [Docker] and [Singularity].

## 1. Introduction

In the Docker-world, "A Container is defined as an instance of an image. \[Which in turn\] An image is an snapshot of a container" [1] . And it is more or less the same in the Singularity-world [2] . In other words, a user can launch a container from an image [3] .

Singularity and Docker platforms provide functionality of virtualization without emphasis of emulation and host OS. In bioinformatic data analysis, much like any other data sciences, these platforms provide containers for packaging of the softwares and their dependencies. These containers can even hold the data required for the specific bioinformatic workflow within the container's environment. This makes it feasible to seamlessly create data analysis environments for reproducibility, mobility, compatibility, and security [2] .

## 2. Singularity

For complete guide on Singularity please refer to: [http://singularity.lbl.gov/quickstart](http://singularity.lbl.gov/quickstart) .

### 2.1 Install

For installation on Linux please follow the guide on: [http://singularity.lbl.gov/install-linux](http://singularity.lbl.gov/install-linux). And for Mac OS X installation it can be installed via Vagrant: [http://singularity.lbl.gov/install-mac](http://singularity.lbl.gov/install-mac) . After the installation, please run ```singularity selftest``` to test the installation. If you've installed singularity using vagrant, the output should look like below:

```bash
vagrant@vagrant:~$ singularity selftest
 + sh -c test -f /usr/local/etc/singularity/singularity.conf                           (retval=0) OK
 + test -u /usr/local/libexec/singularity/bin/action-suid                              (retval=0) OK
 + test -u /usr/local/libexec/singularity/bin/mount-suid                               (retval=0) OK
 + test -u /usr/local/libexec/singularity/bin/start-suid                               (retval=0) OK
```

### 2.2 Download an image

There are two commands to download pre-built Singularity image: ```pull``` and ```build```. ```Pull``` is basically similar to cloning a repositories. While ```pull``` is *the* go to command to download a prebuilt image, one can also use ```build``` to download image. Other than renaming the container, ```build``` also converts the container to the latest format. Both of them can be used for Docker image retrieval as well.

To download an image with these commands:

```bash
# Example for URI shub://vsoch/hello-world
# If a new name is not set for pull, it will use the name from image_URI
$ singularity pull --name [new_optional_name_for_image] [image_URI]
# When using build, image name is mandatory
$ singularity build [image_name_and_path] [image_URI]
```

- ```pull``` example:

```bash
vagrant@vagrant:~$ singularity pull --name Raawwwr.simg shub://vsoch/hello-world
Progress |===================================| 100.0% 
Done. Container is at: /home/vagrant/Raawwwr.simg
vagrant@vagrant:~$ ./Raawwwr.simg 
RaawwWWWWWRRRR!!
```

- ```build``` without root access will show a *warning* that some functionality might be missing, but it will run nevertheless. It'll take longer time to download an image using build, due to converting it to converting it to latest release. Example:

```bash
vagrant@vagrant:~$ singularity build Raawwwr_build.simg shub://vsoch/hello-world
Building into existing container: Raawwwr_build.simg
Cache folder set to /home/vagrant/.singularity/shub
Progress |===================================| 100.0% 
Building from local image: /home/vagrant/.singularity/shub/vsoch-hello-world-master.simg
WARNING: Building container as an unprivileged user. If you run this container as root
WARNING: it may be missing some functionality.
Building Singularity image...
Singularity container built: Raawwwr_build.simg
Cleaning up...
vagrant@vagrant:~$ ./Raawwwr_build.simg 
RaawwWWWWWRRRR!!
```

### 2.3 Build an image from scratch

TBA

### 2.4 Interact with an image

TBA

## 3. Docker

TBA


[Docker]: https://www.docker.com/
[Singularity]: http://singularity.lbl.gov/
[1]: http://paislee.io/how-to-automate-docker-deployments/
[2]: http://singularity.lbl.gov/
[3]: https://docs.docker.com/get-started/
