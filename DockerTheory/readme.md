###################################################################################################
### Docker Step-by-Step Guide
### Creator – Pratik Kishor Munot
### Email id – pmunot11@gmail.com / pmunot@slb.com
### Version – 1.1
### Readme – This document is created by Pratik Munot for basic understanding of Docker Theory
### Last Updated – 31st May, 2023
##################################################################################################

# History and Motivation

<!-- no toc -->
  - [Docker Installation Steps on RHEL 7](#Docker-installation-Steps-on-RHEL-7)
  - [What is a container?](#what-is-a-container)
  - [History of virtualization](#history-of-virtualization)
    - [Bare Metal](#bare-metal)
    - [Virtual Machines](#virtual-machines)
    - [Containers](#containers)
    - [Tradeoffs](#tradeoffs)

---

### Docker installation Steps on RHEL 7
A way to package application with all the necessary dependencies and configuration
It’s a portable artifact that can be easily shared and moved around

1.	Login to RHEL Linux VM
2.	Type the following command to install Docker via yum provided by Red Hat:
sudo yum install docker
3.	Type the following command to remove old version of Docker:
sudo yum remove docker docker-common docker-selinux docker-engine
4.	Type the following command to install the latest version of Docker CE (community edition):
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
5.	sudo yum install docker-ce
6.	Check the version of docker to verify the installation
docker –version
7.	Start docker daemon process by running cmd
systemctl start docker
8.	Run docker version cmd to check both client and server are running properly

src - https://www.cyberciti.biz/faq/install-use-setup-docker-on-rhel7-centos7-linux/





## What is a container?

A Docker container image is a lightweight, standalone, executable package of software that includes everything needed to run an application (https://www.docker.com/resources/what-container/).

## History of virtualization

### Bare Metal

Before virtualization was invented, all programs ran directly on the host system. The terminology many people use for this is "bare metal". While that sounds fancy and scary, you are almost certainly familiar with running on bare metal because that is what you do whenever you install a program onto your laptop/desktop computer. 

![](./assets/bare-metal.jpg)

With a bare metal system, the operating system, binaries/libraries, and applications are installed and run directly onto the physical hardware.

This is simple to understand and direct access to the hardware can be useful for specific configuration, but can lead to:
- Hellish dependency conflicts
- Low utilization efficiency
- Large blast radius
- Slow start up & shut down speed (minutes)
- Very slow provisioning & decommissioning (hours to days)

---

### Virtual Machines

Virtual machines use a system called a "hypervisor" that can carve up the host resources into multiple isolated virtual hardware configuration which you can then treat as their own systems (each with an OS, binaries/libraries, and applications).

![](./assets/virtual-machine.jpg)

This helps improve upon some of the challenges presented by bare metal:

- No dependency conflicts
- Better utilization efficiency
- Small blast radius
- Faster startup and shutdown (minutes)
- Faster provisioning & decommissioning (minutes)

---

### Containers

Containers are similar to virtual machines in that they provide an isolated environment for installing and configuring binaries/libraries, but rather than virtualizing at the hardware layer containers use native linux features (cgroups + namespaces) to provide that isolation while still sharing the same kernel.

![](./assets/container.jpg)

This approach results in containers being more "lightweight" than virtual machines, but not providing the save level of isolation:

- No dependency conflicts
- Even better utilization efficiency
- Small blast radius
- Even faster startup and shutdown (seconds)
- Even faster provisioning & decommissioning (seconds)
- Lightweight enough to use in development!

---

### Tradeoffs

![](./assets/tradeoffs.jpg)

***Note:*** There is much more nuance to “performance” than this chart can capture. A VM or container doesn’t inherently sacrifice much performance relative to the bare metal it runs on, but being able to have more control over things like connected storage, physical proximity of the system relative to others it communicates with, specific hardware accelerators, etc… do enable performance tuning

