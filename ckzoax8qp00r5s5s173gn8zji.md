## Install Docker on a Raspberry Pi

Are you know it's possible to run Docker on a Raspberry Pi?? My first reaction was surprise since I thought Docker was only for servers. But that notion was incorrect.

Let's begin with a definition of Docker.

## What is Docker?

[Docker](https://www.docker.com/) is an [open-source project](https://github.com/docker/docker) for automating the deployment of applications as portable, self-sufficient containers that can run anywhere. 

Docker containers can run anywhere, on-premises in the customer data center, in an external service provider, or in the cloud. Docker image containers can run natively on Linux and Windows. However, Windows images can run only on Windows hosts and Linux images can run on Linux hosts and Windows hosts.

## Why Should you install Docker on a Raspberry Pi?
It's a pretty common question. 
### Consistent & Isolated Environment
Docker's first advantage is that it provides you with a consistent and isolated environment. It takes care of isolating and separating your apps and resources in such a way that each container is able to access all the necessary resources without interfering with or affecting another container.
### Better Portability
Additionally, Docker's portability is a tremendous benefit. Applications built with Docker containers are extremely portable. 
### Cost-Effective
In addition, Docker improves resource utilization, so low-end clients like Raspberry Pis can do more.
### Security
As a final advantage, we have the security aspect! In a nutshell, a containerized application is more secure than one that runs on bare metal. Because Docker takes care of complete isolation and segregation of the applications running within the containers, it gives developers complete control over traffic. Data from one container cannot be accessed by another without authorization. Besides that, each container is assigned its own set of resources. It is essential to remember that you cannot rely on Docker containers alone to take appropriate security measures. In order to ensure overall security, you will also need to consider other security areas. 

Now it's time to follow the below steps to install Docker
## Installing Docker
### Get `get-docker` script 
`get-docker` script is a script that docker wrote to install docker on any system that could install become simplified 
```
wget -O get-docker.sh https://get.docker.com
```
### Run the `get-docker` script
To run the `get-docker` script you must run the below command 
```
sudo sh get-docker.sh
```
wait until the script is fully executed 
### See the result 🤩
run the `docker -v` command. you must a result like this 
```
Docker version 20.10.12, build e91ed57
```
## Summary
You can use the comment section below to let me know if you have any questions or issues! I'm here to help.