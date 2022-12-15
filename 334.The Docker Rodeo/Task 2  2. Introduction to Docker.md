2.1. What is Docker?

Starting in 2013, Docker was introduced to solve the costly and time-consuming process of application development and service delivery. Docker employs what is currently a "hot potato" topic for developers: containerization, this technology separates applications into their own containers, where they share the resources of, but interact with the operating system independently of each other.  

**Docker:**

-   Is extremely portable, if a computer can run Docker, it can run a Docker container. This means that developers only have to write the application once for multiple devices - a very big headache solved!
-   Has a considerably less resource usage per-container then Virtual Machines (VMs) I.e. RAM and CPU (we'll come onto this later)
-   Allows you to set up a complex environment in a few simple steps through Dockerfiles (again, we'll come onto this later)
-   Is most importantly, very lucrative to a pentester as containerization has been so widely adopted in information technology today.

2.2. What are Docker "containers" & why are they used?

As we previously mentioned, containers share computing resources but remain isolated enough to not conflict with one another via the Docker engine. These containers don't run a fully-fledged operating system, unlike a VM. Let's look at the diagram below for a better picture:

![](https://assets.tryhackme.com/additional/docker-rodeo/t2/docker%20containers2.png)

We can see three containers running their own applications with no virtualisation. The three applications are isolated from one another, but use the main operating system's resources. Whereas, in comparison to running these applications in virtual machines:

![](https://assets.tryhackme.com/additional/docker-rodeo/t2/vm-layers3.png)  

The "_Guest Operating System_" is where the resources are used up. For example,  a recommended minimum install size of Ubuntu is 20gb, if you were to run this for three applications, you'd require 60GB of storage. Whereas, a Ubuntu Docker image has the base size of around 180MB~. Containers can share base images too! Extremely space-efficient.  

2.3. What are Docker Images?

Explaining the details of how docker containers are made aren't a requirement of this room. We do, however, need to understand some basic principles for later tasks. Docker containers are created from Docker images; consider these images as instruction manuals telling you how to assemble a piece of furniture.

These files contain commands such as `RUN`and `COPY`that will be executed by the container. `RUN`commands will execute system commands such as `apt-get` or `ls /home/`  

![](https://assets.tryhackme.com/additional/docker-rodeo/t2/docker-image.png)

Answer the questions below

Does Docker run on a Hypervisor? (Yay/Nay)
	
	Nay