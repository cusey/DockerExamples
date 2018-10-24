# Use Case 2 : 
# Host a website on NGINX HTTP Server

## Step 1: Building an image

**Sytax:**  

```
docker build -t <image-name> <location of dockerfile>
```
**Example:**

```
Johns-MacBook-Pro:Case2 johncusey$ cd /Users/johncusey/OneDrive/Documents/GitHub/DockerExamples/Case2

Johns-MacBook-Pro:Case2 johncusey$ docker build -t hello-world-html  .

Sending build context to Docker daemon  14.85kBStep 1/4 : FROM nginx:1.14 ---> ecc98fc2f376
Step 2/4 : LABEL "Maintainer"="Cusey"
 ---> Running in 4de55d96ba4b
Removing intermediate container 4de55d96ba4b
 ---> a1904ce0421f
Step 3/4 : COPY default.conf /etc/nginx/conf.d/
 ---> 84fc1ede8eef
Step 4/4 : COPY hello-world-html/ /usr/share/nginx/html/hello-world-html
 ---> e86aefe80c78
Successfully built e86aefe80c78
Successfully tagged hello-world-html:latest

```
## Step 2: List all the images
**Syntax:**   

```
docker images
```
**Example**   

```
Johns-MacBook-Pro:Case2 johncusey$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello-world-html    latest              e86aefe80c78        3 minutes ago       109MB
<none>              <none>              2ba3792a942e        5 minutes ago       109MB
nginx               1.14                ecc98fc2f376        8 days ago          109MB
```

## Step 3: Running a container from the image
**Syntax:**

```
docker run -itd --name <container-name> -p <host-port>:<port-in-container> image-name:tag
```

* -d : represents (detached mode), note that if you dont run this in detached mode, the life of the container will be the life of the terminal in which you are executing it.
* -p : represents the host-port to container-port mapping, if you substitute it with -P you will get a random port allocated by docker
* --name : represents the name of the container 

**Example**  

```
Johns-MacBook-Pro:Case2 johncusey$ docker run -itd --name my-nginx-container-1 -p 7777:80 hello-world-html:latest
cd6777560c34d01601de51e91b7ba37122a277c947b6044824b03efb6dea8f8d

Johns-MacBook-Pro:Case2 johncusey$ docker run -itd --name my-nginx-container-2 -p 7778:80 hello-world-html:latest
23bd60b542108cb59360f3f331885b6169041bd903294dd12aa5aead0ce806b5
```