# Docker
Docker is an open-source project designed to make it easier to create, deploy, and run applications using **containers**. Docker solves the problem of an application needing to be built and packaged in many different forms to be able to run on different machines and operating systems. Docker solves this problem by packaging up an application's code with all of its dependencies along with an OS, and guaranteeing that this Docker image will run identically no matter what machine it is run on.

## Computer Architecture
* Every computer composed of 4 key parts:
  * Processor (CPU)
  * Memory (RAM)
  * Storage (Hard Disk/SSD)
  * Network Card (NIC)
* Main task of **operating system** is to manage these 4 resources between the applications using your computer.
* The **kernel** is the first program loaded when the computer is turned on, and has the core responsibility of controlling the hardware.

## Containers
* A standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another. 
* A *Docker container image* is a lightweight, standalone, executable package of software that includes everything needed to run an application including: code, runtime, system tools, system libraries and settings.
* Allow a developer to package up an application with all of the parts it needs, such as libraries and other dependencies, and ship it all out in one package.
* Containers are extremely *lightweight* because they do not contain the extra baggage of a **virtual machine** - additional resources that applications do not need to run. Specifically, they do not require a **Hypervisor**.
  * The Hypervisor is what enables virtualization (running multiple operating systems on one physical machine) 
* Essentially a container is a virtual machine that does not include a kernel.
* The definition of a container is that it is an instance of an **image** running as a process on your machine.

## Images
* An image is that application itself that we want to run, such as Node, Ruby, or Postgres.
* A Docker image generally consists of a collection of files, libraries, and dependencies. 