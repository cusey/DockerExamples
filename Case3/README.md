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
Johns-MacBook-Pro:Case2 johncusey$ cd /Users/johncusey/OneDrive/Documents/GitHub/DockerExamples/Case3

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
```  

## Step 3: Running a container from the image. 

**Syntax:**

```
docker run -itd --name <container-name> 
```
**Example**  

```
Johns-MacBook-Pro:Case2 johncusey$ docker run -itd --name my-java-docker
```   


## Step 4: Look at the log files 

**Syntax:**

```
docker logs -ft  <container-id> 
```
**Example**  

```
Johns-MacBook-Pro:Case2 johncusey$ docker logs -ft  <container-id> 
```

## Step 5: Login into the container to see the file structure   

**Syntax:**   

```
docker exec -it  <container-id> /bin/bash
```
**Example**     

```
Johns-MacBook-Pro:Case2 johncusey$ docker exec -it  <container-id> /bin/bash

#ls

# cd /usr/local/docker-git-hello-world

# cd /usr/local/docker-git-hello-world/target 

#exit
```    

## Link your DockerHub with your GitHub repository   





