#  Use Case 3 : Docker-Git integration and creating a custom UBUNTU image

Use case 3 : Run a simple java Hello World Program


## Setup 1: the Eclispe IDE and building Maven Project    

Setup workspace were the github repository is located.   

![Setup Workspace](https://github.com/cusey/ImageForWiki/blob/master/DockerExamples/Case3/Eclipse_workspace.png)

Create new Maven Project     

![Create Maven Project](https://github.com/cusey/ImageForWiki/blob/master/DockerExamples/Case3/Eclipse_create_maven.png)   

Click Next  

![Maven Setttings](https://github.com/cusey/ImageForWiki/blob/master/DockerExamples/Case3/Eclipse_maven_setting.png)   

Select maven-archetype-quickstart 1.1   

![Maven Achetype](https://github.com/cusey/ImageForWiki/blob/master/DockerExamples/Case3/Eclispe_maven_achetype.png)    

Select the following Maven Achetype Parameters    

![Maven Achetype Parameter](https://github.com/cusey/ImageForWiki/blob/master/DockerExamples/Case3/Eclipse_maven_archetype_para.png)

## Setup 2: Build images using the Dockerfile

**Sytax:** 
```
docker build -t <image-name> <location of dockerfile>
```
**Example:**

```
Johns-MacBook-Pro:Case2 johncusey$ cd /Users/johncusey/OneDrive/Documents/GitHub/DockerExamples/Case3/docker-git-hello-world

Johns-MacBook-Pro:Case2 johncusey$ docker build -t my-java-docker  .

```   

## Step 3: List all the images
**Syntax:**   

```
docker images
```
**Example**   

```
Johns-MacBook-Pro:Case2 johncusey$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
my-java-docker      latest              fe8d5fee0fa4        24 seconds ago      1.06GB
ubuntu              16.04               4a689991aa24        13 days ago         116MB
```  

## Step 3: Running a container from the image. 

**Syntax:**

```
docker run -itd --name <container-name> 
```
**Example**  

```
Johns-MacBook-Pro:docker-git-hello-world johncusey$ docker run -itd  my-java-docker
fd99b105d27508e40a936066a666a3173bec235de1faaf63e9d72548bad77a7c
```   


## Step 4: Look at the log files 

**Syntax:**

```
docker logs -ft  <container-id> 
```
**Example**  

```
Johns-MacBook-Pro:docker-git-hello-world johncusey$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
fd99b105d275        my-java-docker      "java -cp /usr/local…"   43 seconds ago      Up 41 seconds                           affectionate_keldysh
Johns-MacBook-Pro:Case2 johncusey$ docker logs -ft  fd99b105d275
2018-11-01T21:51:06.342503900Z Hello World Ping 0
2018-11-01T21:51:07.344042100Z Hello World Ping 1
2018-11-01T21:51:08.345261400Z Hello World Ping 2
2018-11-01T21:51:09.345808100Z Hello World Ping 3
2018-11-01T21:51:10.349051200Z Hello World Ping 4
2018-11-01T21:51:11.349997800Z Hello World Ping 5
2018-11-01T21:51:12.350460400Z Hello World Ping 6
2018-11-01T21:51:13.351539800Z Hello World Ping 7
2018-11-01T21:51:14.352122000Z Hello World Ping 8
2018-11-01T21:51:15.353218400Z Hello World Ping 9
2018-11-01T21:51:16.354056900Z Hello World Ping 10
```

## Step 5: Login into the container to see the file structure   

**Syntax:**   

```
docker exec -it  <container-id> /bin/bash
```
**Example**  

Run the following commands before the for in the HelloWorldPing class stops running

```
Johns-MacBook-Pro:Case2 johncusey$ docker exec -it  fd99b105d275 /bin/bash

root@fd99b105d275:/# ls
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var

root@fd99b105d275:/# cd /usr/local/docker-git-hello-world
Dockerfile  pom.xml  src  target

root@fd99b105d275:/# cd /usr/local/docker-git-hello-world/target 
root@fd99b105d275:/# ls
archive-tmp  classes  docker-git-hello-world-0.0.1-SNAPSHOT-jar-with-dependencies.jar  docker-git-hello-world-0.0.1-SNAPSHOT.jar  maven-archiver  maven-status
#exit
```    

## Link your DockerHub with your GitHub repository   





