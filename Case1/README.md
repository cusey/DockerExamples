# Use Case 1 : 
# Host a website on Apache httpd Server

## Step 1: Building an image  

### Sytax:

```
docker build -t <image-name> <location of dockerfile>

``` 

### Example:

```
Johns-MacBook-Pro:Case1 johncusey$ docker build -t hello-world-html . 
Sending build context to Docker daemon  28.67kB
Step 1/4 : FROM httpd:latest
latest: Pulling from library/httpd
f17d81b4b692: Pull complete
06fe09255c64: Pull complete
0baf8127507d: Pull complete
1e5b6ba3cfcc: Pull complete
f09ae565a639: Pull complete
Digest: sha256:378951edb85bfd57ddaf2edf482ec62e552667bfc4deeaf326342d481ac526f0
Status: Downloaded newer image for httpd:latest
 ---> 0240c8f5816c
Step 2/4 : LABEL "Maintainer"="Cusey"
 ---> Running in 3ee954e3b2c5
Removing intermediate container 3ee954e3b2c5
 ---> d8dfbdd1b0ef
Step 3/4 : COPY hello-world-html/ /usr/local/apache2/htdocs/hello-world-html
 ---> b49b36d5648b
Step 4/4 : COPY httpd.conf /usr/local/apache2/conf
 ---> 485e67eb9de2
Successfully built 485e67eb9de2
Successfully tagged hello-world-html:latest  

```


```   ```   

## Step 2: List all the images  

#### Syntax: 

``` 
docker images 

```  

### Example

```
Johns-MacBook-Pro:Case1 johncusey$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello-world-html    latest              485e67eb9de2        8 minutes ago       132MB
httpd               latest              0240c8f5816c        4 days ago          132MB

```