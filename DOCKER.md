
# DOCKER  
### Ques 1. What are Containers?
Ans :- Containers are a lightweight and portable form of virtualization technology that allows you to run applications and their dependencies in a consistent and isolated environment. A container packages an application along with all its required libraries, dependencies, and configuration files into a single package. This package, known as a container image, is self-contained and can be executed on any system that supports containerization.

### Ques 2. What are images?
Ans :- In the context of Docker, an image is a lightweight, standalone, and executable package that contains everything needed to run an application, including the code, runtime, libraries, and dependencies. It serves as a template or blueprint for creating and running containers.

### Ques 3. What is docker ?
Ans :- Docker is an open-source platform that enables developers to automate the deployment and management of applications using containerization. It provides a way to build, package, and distribute applications and their dependencies into lightweight and portable containers.

Docker was released in 2013 and quickly gained popularity due to its ease of use and powerful features. It leverages operating system-level virtualization to provide isolated execution environments, known as containers, that encapsulate an application along with its dependencies.

### Ques 4. Why do you need docker?
*  Compatibility/Dependency
*  Long setup time
*  Different Dev/Test/Prod environments

Suppose you have 4 services running web, backend , redis, db on a virtual machine.So it become much difficult to handle that. If you front end need some dependency which can cause damage to your other services. You have some environment variable and key is same for other services. So managing this become much difficult.

By using Docker to containerize your services, you can overcome the challenges of managing dependencies, isolating services, and handling configuration differences. It simplifies the deployment and management of your services, enhances security, and improves scalability.

### Ques 5. What can it do?
* Containerize Applications
* Run each service with itsown dependencies in separate container.


## Basic commands of docker.
* Used to check the version of docker. 
``` 
docker --version 
```
* List running containers
``` 
docker ps 
``` 
* pull docker will pull image from the docker .
``` 
docker pull hello-world 
``` 
* used run a container and if the image does not exist it will pull it and run it.
```
docker run hello-world
```
* Used to run the image with specific version or tag.
```
docker run redis:4.0
```
* List running containers and previously stoped container
``` 
docker ps -a 
```
* Used to stop a running container , You must provide a container-ID or name
```
docker stop <containerID>
```
* Used to delete the container, After running the container it will stay and take the storage
```
docker rm <containerID>
```
* Used to list images 
```
docker images
```
* Used to delete Image, Note that you must stop the container or delete the container before delete the image.
```
docker rmi <image_name>
```
* If the container does not have any running process the conatiner will get exit automatically. Because container are meant to run a specific task.

* When you run a container and if a process is running your the proccess will stay in the terminal but if you want a container to run in the backgruond or attach that backgruond proccess again to your terminal 

* Used to run a container in background
```
docker run -d ubuntu

Output:- aeyf748fh7eedh47dye7f7e47gfd
```
* Attach the background container again to your terminal either by providing the full ID or first few character 
```
docker attach aeyf
```
* Suppose you have a simple app.sh file that take input from the user and print the output with the name. 
When you run the container the it will simple print hello . It will not take any input 'your name' it will just print 'hello'.
Like this 
```
[root@fedora saharsh]# docker run kodekloud/simple-prompt-docker
Welcome! Please enter your name: 
Hello and Welcome !
[root@fedora saharsh]# 
```
Docker does not have terminal to read input. By default docker runs in non interactive mode. You must map your host to dokcer container using the -i parameter.
```
docker run -i kodekloud/simple-prompt-docker
```
For interactive mode.

Use this for interactive terminal.
```
docker run -it kodekloud/simple-prompt-docker
```
### Docker run :- PORT Mapping 
Docker Host or Docker engine.
* The underlying host where the docker is installed is called docker host or docker engine.
* when you runs any application inside your docker container you can access it by going inside your container by if we want to access it other the container on our machine you have map the docker port address to your port address.
* Suppose your application inside docker runs on 3333 port you map it to 8000 or what ever port you want.
```
docker run -p 1001:5000 kodekloud/webapp
```
* you can run multiple container of same image on diffrent diffrent port.

### Docker Volume Mapping
* if you running 
```
docker run mysql
```
* if you do 
```
docker stop mysql 
docker rm mysql 
```
* all the data inside the container is going to lost because we have deleted the conatiner but if you  mount the container directory to your system directory. Then even if you delete the container the data will remain.
```
docker run –v /opt/datadir:/var/lib/mysql mysql
```
### Docker inspect
* docker ps conatiner is enough to get some specific information of your container but if you want to get all the information of your conatiner.
```
docker inspect <container_name>
```
* It will return the data in the JSON formate.

### Container LOGS
* Used to print the logs of a container.
```
docker logs <container name>
```

* Docker build follows an Layered acrhitecture.
* Used to check the history for example if you build an image you write 5 instruction so check the each instruction and the MB that each comand used.
* This Layered acrhitecture helps in building the docker image for example if building of an docker image fails so docker will not build the entire image it will take the step from the cache and runs. It will helps you when you are updating your source code as well.

### Lets create our first image.
https://github.com/saharsh-solanki/invest-it
I used this source code.

```
FROM ubuntu/postgres
RUN apt-get update
RUN apt-get install python3-dev python3-setuptools -y
RUN apt-get install python3-pip -y 
RUN pip install --upgrade pip
RUN apt install python3.10-venv -y
RUN apt-get install libtiff5-dev libjpeg8-dev -y
WORKDIR /opt
COPY . /opt
RUN cd /opt 
RUN python3 -m venv venv
RUN . venv/bin/activate
RUN pip3 install -r /opt/requirements.txt
ENTRYPOINT python3 manage.py runserver
```

### Docker environment variables
* Used this comand to set an env variable
```
-e VAR_KEY=value
```

### Docker CMD vs ENTRYPOINT
When running an Ubuntu container without any additional instructions or a terminal attached, the container will exit immediately because it has no ongoing processes to keep it running. By default, containers are designed to execute a specific command or process and then exit once that task is completed.

Suppose you run ubuntu image with the **docker run ubuntu sleep 10** container is going to be alive for 10 sec and after that it is going to close. 

If you create a docker file you need specify what you are going to do when the container runs. You can do that whith CMD or ENTRYPOINT intruction in the dockerfile.

```
FROM ubuntu
CMD ["sleep","10"] or CMD sleep 10
```

So whenever you are going to run this container by default this command will run.
Yes, You can overide this command as well 

```
docker run custom_image sleep 20
```
So, Sleep 10 is going to replaced with the sleep 20 

But in the case of ENTRYPOINT
```
FROM ubuntu
ENTRYPOINT ["sleep"]
```
It is going to append that new argument from the command.
```
docker run custom_image 20
```

OK, But if you don't provide any argument its is going to throw error that sleep command must require an argument.

So you can do something like this.
```
FROM ubuntu
ENTRYPOINT ["sleep"]
CMD ["10"]
```

if you don't provide this arg. CMD 10 is going to appended and if you provide an arg. that will replace with this CMD.


## Docker Compose 
### What is docker Compose ?
Docker Compose is a tool that allows you to define and manage multi-container Docker applications. It uses YAML files to configure the services, networks, and volumes of your application, making it easy to define complex setups and dependencies.

### here are the few things you need to know when working with docker compose.
* **YAML File:** Docker Compose uses a YAML file (usually named docker-compose.yml) to define your application's configuration. This file describes the services, networks, and volumes required for your application.

**Docker file version**

Version 1: This is the initial version of Docker Compose and has limited functionality. It does not support certain features like networks, volumes, and health checks. It is recommended to use a newer version if possible.

Version 2.x: This version introduced several enhancements over version 1 and is widely used. It supports networks, volumes, build context, and more. Version 2.x is divided into sub-versions like 2.0, 2.1, 2.2, etc., each adding new features and improvements.

Version 3.x: Version 3 of Docker Compose is an evolution of the previous versions and is designed to be compatible with Docker Swarm mode. It includes features specific to Swarm deployments, such as replicas, placement constraints, and rolling updates.

Version 3.8: Version 3.8 supports all the features of earlier versions and provides compatibility with the latest Docker Engine features.

* **Services**: A service is a containerized application or component within your application. Each service in Docker Compose is defined as a separate block in the YAML file. You can specify the image to use, environment variables, ports to expose, and other configuration options for each service.

* **Networks:** Networks allow services within Docker Compose to communicate with each other. By default, Compose sets up a default network for your application, but you can also define custom networks to isolate or group specific services together.

* **Volumes:** Volumes provide persistent storage for your containers. You can define named volumes or bind mounts in Docker Compose to store data or share files between containers and the host system.

* **Build Context:** Docker Compose supports building custom images using a build context. You can specify a build context for a service, which includes the Dockerfile and any necessary files. Compose will build the image before starting the service.

* **Environment Variables:** You can set environment variables for your services in the Docker Compose file. TheseThese variables can be used within containers to configure application settings or pass data between services.

* **Dependencies and Links:** Docker Compose allows you to define dependencies between services. You can specify that one service depends on another, and Compose will start them in the correct order. Additionally, you can establish links between services to enable communication using container names as hostnames.

* **Scaling:** With Docker Compose, you can scale services horizontally by specifying the desired number of replicas. Compose will create and manage the specified number of containers for the service.

* **Command-Line Interface (CLI):** Docker Compose provides a command-line interface that allows you to manage your application. You can use commands like docker-compose up, docker-compose down, and docker-compose ps to start, stop, and check the status of your application.

* **Integration with Docker Swarm:** Docker Compose can also be used with Docker Swarm mode to deploy multi-container applications across multiple machines, creating a swarm of Docker nodes.

* ** Here is the simple docker-compose.yaml file i have wrote ** 
```
version: '3'
services:
  web:
    build: .
    environment:
      DATABASE_HOST: database
    depends_on: 
      - database
    ports: 
      - "8000:8000"

  database:
    image: postgres
    environment:
      POSTGRES_PASSWORD: postgres
      POSTGRES_DB: expert_academy
      
```
* The file starts with the version field set to '3', indicating that it uses version 3 of the Docker Compose specification.

```
version: '3'
```
* web service: This service is defined with the name web. It uses the current directory (.) as the build context for building the image. It also sets an environment variable DATABASE_HOST with the value database. The depends_on field specifies that this service depends on the database service. The ports field maps port 8000 of the host to port 8000 of the container.
```
services:
  web:
    build: .
    environment:
      DATABASE_HOST: database
    depends_on: 
      - database
    ports: 
      - "8000:8000"
```

* 
database service: This service is defined with the name database. It uses the postgres image from the Docker Hub. It sets two environment variables: POSTGRES_PASSWORD with the value postgres and POSTGRES_DB with the value expert_academy.


```
 database:
    image: postgres
    environment:
      POSTGRES_PASSWORD: postgres
      POSTGRES_DB: expert_academy
```

**default network** 
By default, Docker Compose creates a network for your services defined in the docker-compose.yml file. This default network allows containers within the same Compose project to communicate with each other using their service names as hostnames.

When you define services in Docker Compose without explicitly specifying a network, they are automatically connected to the default network. This network is isolated and local to the project.

The default network is created with the project name as a prefix followed by an underscore (_). For example, if your project name is myapp, the default network created by Docker Compose would be myapp_default.

## Docker Registry
* **Public Registry**

Docker Registry is the platform where all the docker images are available. For example when we pulled an image `nginx` from where does this image comes?

So if you don't provide the username docker uses the `nginx` as the username means `account_username:image_name` `nginx:nginx` , and by default docker uses the host `docker.io` . So the finally it become `docker.io/nginx/nginx`.

* **Private Registry** : Some platform provides the private Registry consept as well so that the image is accesible by the authorized user only. But how can we pull image from the private Registry.

* First you need to login to the private registry
```
docker login private-registry.io
```

then it will as for the username and password.

After that, You can pull imags from this Private registry

```
docker login private-registry.io
```

## Docker engine
Suppose you are instaling docker in to an linux machine, by default docker install 3 diffrent component a) Docker deamon b) RestAPI c) Docker CLI.

**Docker deamon** is the used to manage the background proccess like the port, volumes etc.It runs as a system service and handles container lifecycle operations, such as starting, stopping, and monitoring containers. The Docker daemon also manages the interaction with the host operating system, including resource management, networking, and storage.

**RestAPI** is used to give the instruction to the docker deamon
**Docker CLI** Is used to run the dokcer services by command line.

When you run a Docker container using the Docker CLI, it sends requests to the Docker daemon via the REST API. The Docker daemon then executes the requested operations, such as pulling images, creating containers, managing networking, and more. The response is then returned to the Docker CLI, which displays the relevant information or status.

This client-server architecture allows users to manage Docker containers and images using the Docker CLI or other tools by communicating with the Docker daemon through the REST API.

## Docker Storage 
Docker followed an layered architecture to manage the container, Each instruction in the docker file is the layer. When you create an docker image its an READ only means you you can not modify the layre. 
For example 
```
FROM ubuntu
RUN apt-get install python3 
RUN pip install flask
RUN COPY . /
ENTRYPOINT flast start app.py
```
So there are five layred and once the images is create this will READ only.
Now, When you run container docker will create a 6th layre on the top of the image , This 6th layre is READ and WRITE both 

SO once you coppied the app.py file can i now modify it?
Yes you can modify it docker will create a copy of this file in the new layre.This is all called as COPY ON WRITE macheniusm.

* When you are doing mounting by default docker create a directory inside the `var/lib/docker`

```
docker volume create data_volume
```

This will create a volume inside the 

``` var/lib/docker/volumes/data_volume ```
```
docker run -v data_volume:var/lib/mysql mysql
```
This will mount the underlying hosts vloume/data_volume to the containers var/lib/mysql. This is know as volume mounting.

But if you want to mount the specfic dir instead of var/lib you can just directly pass the 

```
docker run -v directory:var/lib/mysql mysql
```

This is know as bind mount.


There are two types of mounting **volume mount and bind mount**.
If you don't create a volume and run the command docker will automatically create a volume.


### Docker Storage drivers
Docker user storage drivers to perform moving files , change location , mounting .etc.Some common storage drivers are AUFS, ZFS, Overlap, Overlap2, Device mapper .
The selection is based on the type of operating system


### Docker network
When you install docker by default its create three different networks bridge, none, and host. the bridge is the default network a container get attached to . if you want to use a different network you can provide command. 
``` 
docker run ubuntu
``` 
``` 
docker run ubuntu --network=none
``` 
``` 
docker run ubuntu --network=host
``` 
The bridge is the private internal network created by the docker on the host. All container by default attached to this network and they get and internal IP address in the range 172.7 series the container can communicate each other using this IP address. If you want to run this outside the container we need to use the port-mapping concept. 

The second option is to run the container into the host network so that it can be directly accessible to the underlying host without doing any port mapping. But now you cannot run multiple containers on the same port because the port is already in use. 
 **User Defined network** 
We can create our custom user defined network by using comand 

``` 
docker network create --driver bridge --subnet ip custom-Isolated network 

```

### Container Orchestration
With docker we run a single instance of the application, but in case your user getting increase and the instance can not handles the load. You can run another instance of the application. But whatr happens when you have thousands of users , and managing performance , Or if any one of your instance crush you need to again start the instance of the application manually and you need to hire a dedicated enginner to this process. And also what happens if the host dies?


But with help of Orchestration you can create thousands of instance and host.
```
docker service create --replicas=100 nodejs
```

And also link the diffrent host and their instance to each other.

Container orchestration platforms allow you to define and deploy services as a collection of containers. They provide mechanisms to scale services up or down based on demand, ensuring that the right number of containers are running to handle the workload efficiently.

Orchestration tools provide service discovery mechanisms that allow containers to find and communicate with each other. They also offer load balancing capabilities to distribute incoming traffic across multiple containers to achieve better performance and high availability.

Orchestration platforms continuously monitor the health and performance of containers. If a container fails or becomes unresponsive, the orchestration system automatically restarts or replaces it to maintain the desired state and ensure application availability.

Some popular container orchestration platforms include Kubernetes, Docker Swarm, Amazon Elastic Container Service (ECS), Google Kubernetes Engine (GKE), and Microsoft Azure Kubernetes Service (AKS). These platforms offer various features and integrations, and the choice depends on factors such as requirements, familiarity, and infrastructure preferences.


### Docker swarm 

Docker Swarm is Docker's native container orchestration and clustering solution. It allows you to create and manage a swarm of Docker nodes, forming a distributed cluster where containers can be deployed and managed at scale. Docker Swarm provides a simple yet powerful way to orchestrate and scale containerized applications.

So for example your application is running on Host or  on a doctor host but what happened when the user or when the load increases on the host so for the user you can create multiple instances of your application but your instance can be Crush, and even your host can die so in that case we can use docker swarm, in docker swarm threre are one node which is known as a master node or the manager node and the other nodes are connected to this master node and this master node manage the other nodes and the other nodes are known as worker.
