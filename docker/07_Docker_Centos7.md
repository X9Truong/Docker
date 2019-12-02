### Installing Docker on CentOS 7

Introduction

Docker is an application that makes it simple and easy to run application processes in a container, which are like virtual machines, only more portable, more resource-friendly, and more dependent on the host operating system. For a detailed introduction to the different components of a Docker container, check out The Docker Ecosystem: An Introduction to Common Components.

There are two methods for installing Docker on CentOS 7. One method involves installing it on an existing installation of the operating system. The other involves spinning up a server with a tool called Docker Machine that auto-installs Docker on it.

In this tutorial, you’ll learn how to install and use it on an existing installation of CentOS 7.

* Get Docker CE for CentOS

### Install using the repository

Before you install Docker CE for the first time on a new host machine, you need to set up the Docker repository. Afterward, you can install and update Docker from the repository.

#### SET UP THE REPOSITORY

* Install required packages. `yum-utils` provides the `yum-config-manager` utility, and `device-mapper-persistent-data` and `lvm2` are required by the devicemapper storage driver.

`yum install -y yum-utils device-mapper-persistent-data lvm2`

### Configure the docker-ce repo:

`yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo`

## 1. Install docker-ce:

`yum install docker-ce -y`

### Add your user to the docker group with the following command.

`sudo usermod -aG docker $(whoami)`

### Set Docker to start automatically at boot time:

`systemctl enable docker.service`

### Finally, start the Docker service:

`systemctl start docker.service`

Optional: Enable the `nightly` or test repositories.

These repositories are included in the docker.repo file above but are disabled by default. You can enable them alongside the stable repository. The following command enables the nightly repository.

`yum-config-manager --enable docker-ce-nightly`

To enable the test channel, run the following command:

`yum-config-manager --enable docker-ce-test`

You can disable the nightly or test repository by running the yum-config-manager command with the --disable flag. To re-enable it, use the --enable flag. The following command disables the nightly repository.

`yum-config-manager --disable docker-ce-nightly`

## 2. Install Docker Compose

* Install Extra Packages for Enterprise Linux

`yum install epel-release -y`

* Install python-pip

`yum install -y python-pip`

* Then install Docker Compose:

`pip install docker-compose`

You will also need to upgrade your Python packages on CentOS 7 to get docker-compose to run successfully:

`yum -y upgrade python*`

* To verify a successful Docker Compose installation, run:

`docker-compose version`

```
[root@devstack ~]# docker-compose version
docker-compose version 1.24.0, build 0aa5906
docker-py version: 3.7.2
CPython version: 2.7.5
OpenSSL version: OpenSSL 1.0.2k-fips  26 Jan 2017
```

