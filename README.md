# DevOps-final_revision

## Docker

* A containerization platform which makes source code portable and deployable across multiple machines.
* Application = source code + environment (libraries, frameworks, platforms, testing tools, build tools, operating system)
* Application Stack
    * Front end, Backend
        * Source code
        * libraries
        * frameworks
        * platforms
        * compilers
        * build tools
        * testing tools
    * Databases
        * drivers
        * servers
    * cache
    * servers (apache tomact, jboss)
    * operating system
* Various profiles in the process of project development to production release: dev | test | uat | pre-production | production
* Docker automates the profile setup process by a concept called containerization which packs source code + environment into something called container.
*  So, simply Docker a tool for packing, deploying and running the applications on any machine.
* Docker file --build--> Docker Image --run--> docker container
* Main components of Docker Architecture:
 1. Docker file (set of instructions to build the Docker Image)
 2. Docker Image (A package which contains the source code and environment details)
 3. Docker Registry (A registry where docker images are available)
 4. Docker client (An implicit component of docker tool which is responsible for docker commands execution)

 * Installing Docker on Amazon Linux machine

 ```
 1. Create Linux VM in AWS cloud
 2. Launch mobxterm tool connecting to the above VM
 3. Execute the following commands

 #update the yum package manager
 $ sudo yum update -y

 #install docker
 $ sudo yum install docker -y

 #start the docker server
 $ sudo service docker start

 #add current user to the docker group
 $ sudo usermod -aG docker ec2-user

 #get info about docker tool
 $ docker info 
 //access permission error
 
 #)restart mobxterm session
 $ exit
 'R' //for restarting

 $ docker info
 // gives info now

```

* Docker commands

```
#to get info about docker tool
$ docker info

#to display list of docker images
$ docker images

#to pull a docker image from the docker hub (docker registry)
$ docker pull <imageid>
or 
$ docker pull <imagename>

#to pull the readymade hello world image
$ docker pull hello-world

#to delete a docker image
$ docker rmi <imageid>
or
$ docker rmi <imagename>
//$docker rmi hello-world

#to run docker container
$ docker run <imageid>
or 
$ docker run <imagename>
//$docker run hello-world

#to get all active/running docker containers
$ docker ps

#to get all docker containers (active and stopped)
$ docker ps -a

#to remove the docker container
$ docker rm <container id>
```

* Running the docker container is nothing but running the application present inside the container over the environment
* Docker clients <-----> Docker Daemon thread <------> Docker registry


```
Docker commands to develop docker file

1. FROM
FROM java:jdk-1.8.0
FROM tomcat:10.0.1
FROM mysql

> Using docker build command that docker file as the input one docker image will be created represented our App/Project, inside this image base images are imported using FROM

2. MAINTAINER
MAINTAINER vignesh <vignesh8ireddy>

3. COPY
COPY <source location> <destination location>

4. ADD
ADD <source> <destination>

5. RUN
RUN <command syntax>
RUN mkdir workspace1
RUN YUM install git
RUN yum install maven

6. CMD
CMD JAVA -jar App.jar


/*

i. create docker file

$vi dockerfile1

FROM ubuntu
MAINTAINER vignesh <vignesh8ireddy@gmail.com>
RUN echo "1st run"
RUN echo "2nd run"
CMD echo "1st cmd"
CMD echo "2nd cmd"
RUN echo "3rd run"
CMD echo "3rd cmd"
CMD echo "4th cmd"

esc --> .wq

ii. build docker image form docker file

$ docker build -t dockerimage1 .
$ docker images

iii. run the image to create a container

$ docker run dockerimage1
//output 
1st run
2nd run
3rd run
4th cmd

*/
7. ENTRYPOINT
8. ENV
9. LABEL
10. USER
11. WORKDIR
12. EXPOSE 
13. VOLUME


using other than default name for building dockerimage

$ docker build -f <dockerfilename> -t <dockerimage>

```

* Procedure for keeping docker images in dockerhub.com

```
1. make sure your docker image is ready
$ docker images

2. login to dockerhub via VM terminal
$ docker login
//username:
//password:

3. tag the docker image with a logical name
$ docker tag dockerimage1 vignesh/image1

4. push the image to the docker registry(docker hub) by tagname
$ docker push vignesh/image1
```

* Pulling the docker image from dockerhub.com and running it
```
$ docker pull vignesh/image1
$ docker run vignesh/image1
```

* 