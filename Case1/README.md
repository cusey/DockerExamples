# Use Case 1 : 
# Host a website on Apache httpd Server

## Step 1: Building an image  

**Sytax:**

```
docker build -t <image-name> <location-of-dockerfile>

``` 

**Example:**

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

**Syntax:**

``` 
docker images 

```  

**Example:**

The **httpd** is the image pull down from Docker Hub . The **hello-world-html** is the image that I built.

```
Johns-MacBook-Pro:Case1 johncusey$ docker images


REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello-world-html    latest              485e67eb9de2        8 minutes ago       132MB
httpd               latest              0240c8f5816c        4 days ago          132MB

```

## Step 4: Running a container from the image. Open the Webpage which is served up from the container  

**Syntax:**    

* -d : represents (detached mode), note that if you dont run this in detached mode, the life of the container will be the life of the terminal in which you are executing it.  

* -p : represents the host-port to container-port mapping, if you substitute it with -P you will get a random port allocated by docker

* --name : represents the name of the container   

```
docker run -itd --name <container-name> -p <host-port>:<port-in-container> image-name:tag

```
**Example:**

```
Johns-MacBook-Pro:Case1 johncusey$ docker run -itd --name hello-world-html-container -p 5555:80 hello-world-html:latest

28a1bccffc30b975902920f4374dd3818fcdf9d0d85e7be6b4174b5946056faa

```

![Hello World Webpage](https://github.com/cusey/ImageForWiki/blob/master/DockerExamples/hello-world-html.png)

## Step 5: View all the containers

**Syntax:** 

* Shows all the containers which are running

```
docker ps 

```
* Shows all the containers stopped and running

```
docker ps -a
```

**Example:**

```
Johns-MacBook-Pro:Case1 johncusey$ docker ps   

CONTAINER ID        IMAGE                     COMMAND              CREATED             STATUS              PORTS                  NAMES
28a1bccffc30        hello-world-html:latest   "httpd-foreground"   30 minutes ago      Up 30 minutes       0.0.0.0:5555->80/tcp   hello-world-html-container
```
### Step 6: Inspect the container and image   

**Syntax:** 

```
docker inspect <container-id>
```

**Example:**  

```
Johns-MacBook-Pro:Case1 johncusey$ docker inspect 28a1bccffc30
[
    {
        "Id": "28a1bccffc30b975902920f4374dd3818fcdf9d0d85e7be6b4174b5946056faa",
        "Created": "2018-10-24T00:56:07.196389Z",
        "Path": "httpd-foreground",
        "Args": [],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 2755,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2018-10-24T00:56:07.7618007Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:485e67eb9de2dedc62aae57bd3b8ad3799291804dd20294e266983da3392baee",
        "ResolvConfPath": "/var/lib/docker/containers/28a1bccffc30b975902920f4374dd3818fcdf9d0d85e7be6b4174b5946056faa/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/28a1bccffc30b975902920f4374dd3818fcdf9d0d85e7be6b4174b5946056faa/hostname",
        "HostsPath": "/var/lib/docker/containers/28a1bccffc30b975902920f4374dd3818fcdf9d0d85e7be6b4174b5946056faa/hosts",
        "LogPath": "/var/lib/docker/containers/28a1bccffc30b975902920f4374dd3818fcdf9d0d85e7be6b4174b5946056faa/28a1bccffc30b975902920f4374dd3818fcdf9d0d85e7be6b4174b5946056faa-json.log",
        "Name": "/hello-world-html-container",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "default",
            "PortBindings": {
                "80/tcp": [
                    {
                        "HostIp": "",
                        "HostPort": "5555"
                    }
                ]
            },
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "CapAdd": null,
            "CapDrop": null,
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "shareable",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "ConsoleSize": [
                0,
                0
            ],
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": null,
            "BlkioDeviceWriteBps": null,
            "BlkioDeviceReadIOps": null,
            "BlkioDeviceWriteIOps": null,
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DiskQuota": 0,
            "KernelMemory": 0,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": 0,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware"
            ],
            "ReadonlyPaths": [
                "/proc/asound",
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/27bf067a99666c2149892cdffee82b99f9767b18024eb4abde2fbe65267d757d-init/diff:/var/lib/docker/overlay2/fae95a30989b496c4e951fcefec5b06b1739f7f9583d7ea00bbd5958f4e98d11/diff:/var/lib/docker/overlay2/03c0570081841dcb5ef59ee65ccb766fd23443c04b3bfac74d43ee676c74cc79/diff:/var/lib/docker/overlay2/12b4ef56300691aa80b54ff030b438c7480fc94bc8abb97fde9bdfd16b393fe9/diff:/var/lib/docker/overlay2/4978105da3115a69f875e9a38b899410fed0de6405c1a6d486dbf3c694a130bb/diff:/var/lib/docker/overlay2/5b19d24999ce91f000abf19afc8c969ba2e3487e54667b47236189a138d2d916/diff:/var/lib/docker/overlay2/0ccb1ca333ab2b4f93574cc44a659d071a1a15571ded2766c8cb1ba2a24a4fb3/diff:/var/lib/docker/overlay2/69f4938222799ba3e2f5e9e845f0006730505f416f4df323f63bd96606f95ba5/diff",
                "MergedDir": "/var/lib/docker/overlay2/27bf067a99666c2149892cdffee82b99f9767b18024eb4abde2fbe65267d757d/merged",
                "UpperDir": "/var/lib/docker/overlay2/27bf067a99666c2149892cdffee82b99f9767b18024eb4abde2fbe65267d757d/diff",
                "WorkDir": "/var/lib/docker/overlay2/27bf067a99666c2149892cdffee82b99f9767b18024eb4abde2fbe65267d757d/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "28a1bccffc30",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "80/tcp": {}
            },
            "Tty": true,
            "OpenStdin": true,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/apache2/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "HTTPD_PREFIX=/usr/local/apache2",
                "HTTPD_VERSION=2.4.35",
                "HTTPD_SHA256=2607c6fdd4d12ac3f583127629291e9432b247b782396a563bec5678aae69b56",
                "HTTPD_PATCHES=",
                "APACHE_DIST_URLS=https://www.apache.org/dyn/closer.cgi?action=download&filename= \thttps://www-us.apache.org/dist/ \thttps://www.apache.org/dist/ \thttps://archive.apache.org/dist/"
            ],
            "Cmd": [
                "httpd-foreground"
            ],
            "ArgsEscaped": true,
            "Image": "hello-world-html:latest",
            "Volumes": null,
            "WorkingDir": "/usr/local/apache2",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {
                "Maintainer": "Cusey"
            }
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "04d36bc2761b4f57fc25f7879ff43ce98015a48f21e24eac8ac18c6a4e5fa220",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {
                "80/tcp": [
                    {
                        "HostIp": "0.0.0.0",
                        "HostPort": "5555"
                    }
                ]
            },
            "SandboxKey": "/var/run/docker/netns/04d36bc2761b",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "d88d5f1788e27d06ca23ded0847eea5d6480724da19a451cf6a882a85f3aa05e",
            "Gateway": "172.17.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.17.0.2",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:11:00:02",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "a345c83db11e98fdeed9942fe6e5a05fdf64f2958c022c11108df4eaaeee62dc",
                    "EndpointID": "d88d5f1788e27d06ca23ded0847eea5d6480724da19a451cf6a882a85f3aa05e",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.2",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:02",
                    "DriverOpts": null
                }
            }
        }
    }
]
```

### Step 7: View Container logs    

**Syntax:** 

View the logs of the container   

```
docker logs <container-id>
```
Tail the logs of the container

```
docker logs -ft <container-id>
```

**Example:**  

```
Johns-MacBook-Pro:Case1 johncusey$ docker logs -ft  28a1bccffc30

2018-10-24T00:56:07.768679400Z AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 172.17.0.2. Set the 'ServerName' directive globally to suppress this message
2018-10-24T00:56:07.771821500Z AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 172.17.0.2. Set the 'ServerName' directive globally to suppress this message
2018-10-24T00:56:07.776341700Z [Wed Oct 24 00:56:07.773358 2018] [mpm_event:notice] [pid 1:tid 140571665806528] AH00489: Apache/2.4.35 (Unix) configured -- resuming normal operations
2018-10-24T00:56:07.776369200Z [Wed Oct 24 00:56:07.773565 2018] [core:notice] [pid 1:tid 140571665806528] AH00094: Command line: 'httpd -D FOREGROUND'
2018-10-24T00:58:17.143826000Z 172.17.0.1 - - [24/Oct/2018:00:58:17 +0000] "GET / HTTP/1.1" 200 109
2018-10-24T00:58:17.838989200Z 172.17.0.1 - - [24/Oct/2018:00:58:17 +0000] "GET /favicon.ico HTTP/1.1" 404 209
2018-10-24T00:59:09.265115600Z 172.17.0.1 - - [24/Oct/2018:00:59:09 +0000] "-" 408 -
```

### Step 8: Stop the container