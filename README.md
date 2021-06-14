# Docker

# Getting Started with Docker  
In this chapter, we are going to learn about docker shell, the command line utility and how to use it to
launch containers. We will also learn what it means to run a container, its lifecycle and perform basic
operations such as creating, starting, stopping, removing, pausing containers and checking the status etc.

## Using docker cli  
We can use docker cli to interact with docker daemon. Various functions of docker command is given below. Try this yourself by runnig **$sudo docker** command

```
docker
```

[Output]  
```
Usage: docker [OPTIONS] COMMAND [arg...]
       docker [ --help | -v | --version ]

A self-sufficient runtime for containers.

Options:

  --config=~/.docker              Location of client config files
  -D, --debug                     Enable debug mode
  -H, --host=[]                   Daemon socket(s) to connect to
  -h, --help                      Print usage
  -l, --log-level=info            Set the logging level
  --tls                           Use TLS; implied by --tlsverify
  --tlscacert=~/.docker/ca.pem    Trust certs signed only by this CA
  --tlscert=~/.docker/cert.pem    Path to TLS certificate file
  --tlskey=~/.docker/key.pem      Path to TLS key file
  --tlsverify                     Use TLS and verify the remote
  -v, --version                   Print version information and quit

Commands:
    attach    Attach to a running container
    build     Build an image from a Dockerfile
    commit    Create a new image from a container's changes
    cp        Copy files/folders between a container and the local filesystem
    create    Create a new container
    diff      Inspect changes on a container's filesystem
    events    Get real time events from the server
    exec      Run a command in a running container
    export    Export a container's filesystem as a tar archive
    history   Show the history of an image
    images    List images
    import    Import the contents from a tarball to create a filesystem image
    info      Display system-wide information
    inspect   Return low-level information on a container, image or task
    kill      Kill one or more running containers
    load      Load an image from a tar archive or STDIN
    login     Log in to a Docker registry.
    logout    Log out from a Docker registry.
    logs      Fetch the logs of a container
    network   Manage Docker networks
    node      Manage Docker Swarm nodes
    pause     Pause all processes within one or more containers
    port      List port mappings or a specific mapping for the container
    ps        List containers
    pull      Pull an image or a repository from a registry
    push      Push an image or a repository to a registry
    rename    Rename a container
    restart   Restart a container
    rm        Remove one or more containers
    rmi       Remove one or more images
    run       Run a command in a new container
    save      Save one or more images to a tar archive (streamed to STDOUT by default)
    search    Search the Docker Hub for images
    service   Manage Docker services
    start     Start one or more stopped containers
    stats     Display a live stream of container(s) resource usage statistics
    stop      Stop one or more running containers
    swarm     Manage Docker Swarm
    tag       Tag an image into a repository
    top       Display the running processes of a container
    unpause   Unpause all processes within one or more containers
    update    Update configuration of one or more containers
    version   Show the Docker version information
    volume    Manage Docker volumes
    wait      Block until a container stops, then print its exit code

```

## Getting Information about Docker Setup  
We can get the information about our Docker setup in several ways. Namely,

```
docker -v  

docker version  

docker info  
```

[Output of **docker -v**]  
```
Docker version 1.12.1, build 23cf638
```

[Output of **docker version**]  
```
Client:
 Version:      1.12.1
 API version:  1.24
 Go version:   go1.6.3
 Git commit:   23cf638
 Built:
 OS/Arch:      linux/amd64

Server:
 Version:      1.12.1
 API version:  1.24
 Go version:   go1.6.3
 Git commit:   23cf638
 Built:
 OS/Arch:      linux/amd64
```

[Output of **docker info**]  
```
Containers: 10
 Running: 0
 Paused: 0
 Stopped: 10
Images: 8
Server Version: 1.12.1
Storage Driver: devicemapper
 Pool Name: docker-253:0-135975386-pool
 Pool Blocksize: 65.54 kB
 Base Device Size: 10.74 GB
 Backing Filesystem: xfs
 Data file: /dev/loop0
 Metadata file: /dev/loop1
 Data Space Used: 1.084 GB
 Data Space Total: 107.4 GB
 Data Space Available: 42.22 GB
 Metadata Space Used: 2.052 MB
 Metadata Space Total: 2.147 GB
 Metadata Space Available: 2.145 GB
 Thin Pool Minimum Free Space: 10.74 GB
 Udev Sync Supported: true
 Deferred Removal Enabled: false
 Deferred Deletion Enabled: false
 Deferred Deleted Device Count: 0
 Data loop file: /var/lib/docker/devicemapper/devicemapper/data
 WARNING: Usage of loopback devices is strongly discouraged for production use. Use `--storage-opt dm.thinpooldev` to specify a custom block storage device.
 Metadata loop file: /var/lib/docker/devicemapper/devicemapper/metadata
 Library Version: 1.02.107-RHEL7 (2016-06-09)
Logging Driver: json-file
Cgroup Driver: cgroupfs
Plugins:
 Volume: local
 Network: bridge host null overlay
Swarm: inactive
Runtimes: runc
Default Runtime: runc
Security Options: seccomp
Kernel Version: 3.10.0-327.28.3.el7.x86_64
Operating System: CentOS Linux 7 (Core)
OSType: linux
Architecture: x86_64
CPUs: 1
Total Memory: 1.797 GiB
Name: dockerserver
ID: QV4Z:HQZP:6ANK:PU5X:554Y:JA2Z:TZ54:ODDN:2HYJ:N4LW:WVZF:AG3L
Docker Root Dir: /var/lib/docker
Debug Mode (client): false
Debug Mode (server): false
Registry: https://index.docker.io/v1/
Insecure Registries:
 127.0.0.0/8

```

The **docker info** command gives a lot of useful information like total number of containers and images along with information about host resource utilization

## Launching our first container  
Now we have a basic understanding of docker command and sub commands, let us dive straight into launching our very first **container**

```
docker run alpine uptime
```

Where,

  * we are using docker **client** to
  * run a application/command **uptime** using
  * an image by name **alpine**

[Output]  
```
docker run alpine uptime
Unable to find image 'alpine:latest' locally
latest: Pulling from library/alpine
117f30b7ae3d: Pull complete
Digest: sha256:02eb5cfe4b721495135728ab4aea87418fd4edbfbf83612130a81191f0b2aae3
Status: Downloaded newer image for alpine:latest
 07:45:40 up  3:13,  load average: 0.00, 0.00, 0.00
```

**What happened?**  
This command will

  * Pull the **alpine** image file from **docker hub**, a cloud registry
  * Create a runtime environment/ container with the above image   
  * Launch a program (called **uptime**) inside that container  
  * Stream that output to the terminal  
  * Stop the container once the program is exited

**Where did my container go?**

The point here to remember is that, when that executable stops running inside the container, the container itself will stop  
This process will further be explained under the **lifecycle of a container** topic.

Let's see what happens when we run that command again,

[Output]  
```
docker run alpine uptime
 07:48:06 up  3:15,  load average: 0.00, 0.00, 0.00
```

Now docker no longer pulls the image again from registry, because **it has stored the image locally** from the previous run  
So once an image is pulled, we can make use of that image to create and run as many container as we want without the need of downloading the image again. However it has created a new instance of the image/container.

## Checking Status of the containers  
We have understood how docker run commands works. But what if you want to see list of running containers and history of containers that had run and exited? This can be done by executing the following commands

```
docker ps
```

[Output]  
```
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

This command doesn't give us any information. Because, **docker ps** command will only show list of container(s) which are **running**

```
docker ps -l
```

[Output]  
```
CONTAINER ID        IMAGE               COMMAND             CREATED              STATUS                          PORTS               NAMES
988f4d90d604        alpine              "uptime"            About a minute ago   Exited (0) About a minute ago                       fervent_hypatia
```

The **-l** flag shows the last run container along with other details like image it used, command it executed, return code of that command, etc.,

```
docker ps -n 2
```

[Output]  
```
NAMES
988f4d90d604        alpine              "uptime"            About a minute ago   Exited (0) About a minute ago                       fervent_hypatia
acea3023dca4        alpine              "uptime"            3 minutes ago        Exited (0) 3 minutes ago                            mad_darwin
```

Docker gives us the flexibility to show the desirable number of last run containers. This can be achieved by using **-n #no_of_results** flag

```
docker ps -a
```

[Output]  
```
CONTAINER ID        IMAGE                        COMMAND                  CREATED              STATUS                          PORTS                  NAMES
988f4d90d604        alpine                       "uptime"                 About a minute ago   Exited (0) About a minute ago                          fervent_hypatia
acea3023dca4        alpine                       "uptime"                 4 minutes ago        Exited (0) 4 minutes ago                               mad_darwin
60ffa94e69ec        ubuntu:14.04.3               "bash"                   27 hours ago         Exited (0) 26 hours ago                                infallible_meninsky
dd75c04e7d2b        schoolofdevops/ghost:0.3.1   "/entrypoint.sh npm s"   4 days ago           Exited (0) 3 days ago                                  kickass_bardeen
c082972f66d6        schoolofdevops/ghost:0.3.1   "/entrypoint.sh npm s"   4 days ago           Exited (0) 3 days ago           0.0.0.0:80->2368/tcp   sodcblog
```

This command will show all the container we have run so far.

## Running Containers in Interactive Mode  
We can interact with docker containers by giving -it flags at the run time. These flags stand for

  * i - Interactive  
  * t - tty

```
docker run -it alpine:3.4 sh
```

[Output]  
```
Unable to find image 'alpine:3.4' locally
3.4: Pulling from library/alpine

e110a4a17941: Pull complete
Digest: sha256:3dcdb92d7432d56604d4545cbd324b14e647b313626d99b889d0626de158f73a
Status: Downloaded newer image for alpine:3.4
/ #
```

As you see, we have landed straight into **sh** shell of that container. This is the result of using **-it** flags and mentioning that container to run the **sh** shell. Don't try to exit that container yet. We have to execute some other commands in it to understand the next topic

## Namespaced  
Like a full fledged OS, Docker container has its own namespaces  
This enables Docker container to isolate itself from the host as well as other containers  
Run the following commands and see that alpine container has its own namespaces and not inheriting much from **host OS**

[Command]  
```
cat /etc/issue
```

[Output]  
```
Welcome to Alpine Linux 3.4
Kernel \r on an \m (\l)
```

[Command]  
```
ps aux
```

[Output]  
```
PID   USER     TIME   COMMAND
    1 root       0:00 sh
    6 root       0:00 ps aux
```

[Command]  
```
ifconfig
```

[Output]  
```
eth0      Link encap:Ethernet  HWaddr 02:42:AC:11:00:02
          inet addr:172.17.0.2  Bcast:0.0.0.0  Mask:255.255.0.0
          inet6 addr: fe80::42:acff:fe11:2%32640/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:8 errors:0 dropped:0 overruns:0 frame:0
          TX packets:8 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:648 (648.0 B)  TX bytes:648 (648.0 B)

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1%32640/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
```

[Command]  
```
hostname
```

[Output]  
```
ae84d253ecb5
```

## Shared:  
We have understood that containers have their own namespaces. But will they share something to some extent? the answer is **YES**. Let's run the following commands on both the container and the host machine

[Command]  
```
uname -a
```

[Output - **container**]  
```
Linux ae84d253ecb5 3.10.0-327.28.3.el7.x86_64 #1 SMP Thu Aug 18 19:05:49 UTC 2016 x86_64 Linux
```

[Output - **hostmachine**]  
```
Linux dockerserver 3.10.0-327.28.3.el7.x86_64 #1 SMP Thu Aug 18 19:05:49 UTC 2016 x86_64 x86_64 x86_64 GNU/Linux
```

As you can see, the container uses the same Linux Kernel from the host machine. Just like **uname** command, the following commands share the same information as well. In order to avoid repetition, we will see the output of container alone.

[Command]  
```
date  
```

[Output]  
```
Wed Sep 14 18:21:25 UTC 2016
```

[Command]  
```
cat /proc/cpuinfo
```

[Output]  
```
processor       : 0
vendor_id       : GenuineIntel
cpu family      : 6
model           : 94
model name      : Intel(R) Core(TM) i7-6700HQ CPU @ 2.60GHz
stepping        : 3
cpu MHz         : 2592.002
cache size      : 6144 KB
physical id     : 0
siblings        : 1
core id         : 0
cpu cores       : 1
apicid          : 0
initial apicid  : 0
fpu             : yes
fpu_exception   : yes
cpuid level     : 22
wp              : yes
flags           : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 syscall nx rdtscp lm constant_tsc rep_good nopl xtopology nonstop_tsc pni pclmulqdq monitor ssse3 cx16 sse4_1 sse4_2 movbe popcnt aes xsave avx rdrand hypervisor lahf_lm abm 3dnowprefetch rdseed clflushopt
bogomips        : 5184.00
clflush size    : 64
cache_alignment : 64
address sizes   : 39 bits physical, 48 bits virtual
power management:
```

[Command]  
```
free
```

[Output]  
```
total       used       free     shared    buffers     cached
Mem:       1884176     650660    1233516          0       1860     473248
-/+ buffers/cache:     175552    1708624
Swap:      1048572          0    1048572
```

Now exit out of that container by running **exit** or by pressing **ctrl+d**

## Making Containers Persist

### Running Containers in Detached Mode  
So far, we have run the containers interactively. But this is not always the case. Sometimes you may want to start a container  without interacting with it. This can be achieved by using **"detached mode"** (**-d**) flag. Hence the container will launch the default application inside and run in the background. This saves a lot of time, we don't have to wait till the applications launches successfully. It will happen behind the screen. Let us run the following command to see this in action

[Command]  
```
docker run -d schoolofdevops/loop program
```

-d , --detach : detached mode

[Output]  
```
2533adf280ac4838b446e4ee1151f52793e6ac499d2e631b2c752459bb18ad5f
```

This will run the container in detached mode. We are only given with full container id as the output

Let us check whether this container is running or not

[Command]  
```
docker ps
```

[Output]  
```
CONTAINER ID        IMAGE                 COMMAND             CREATED             STATUS              PORTS               NAMES
2533adf280ac        schoolofdevops/loop   "program"           37 seconds ago      Up 36 seconds                           prickly_bose
```

As we can see in the output, the container is running in the background

## Connecting to running container to execute commands  
We can connect to the containers which are running in detached mode by using these following commands

[Command]  
```
docker exec -it 2533adf280ac sh
```

[Output]  
```
/ #
```

Now exit the container.

## Pausing Running Container  
Just like in a video, it is easy to pause and unpause the running container

[Command]  
```
docker pause 2533adf280ac
```

After running pause command, run docker ps again to check the container status

[Output]  
```
CONTAINER ID        IMAGE                 COMMAND             CREATED             STATUS                  PORTS               NAMES
2533adf280ac        schoolofdevops/loop   "program"           2 minutes ago       Up 2 minutes (Paused)                       prickly_bose
```

## Unpausing the paused container  
This can be achieved by executing following command

[Command]  
```
docker unpause
```

Run *docker ps* to verify the changes

[Output]  
```
CONTAINER ID        IMAGE                 COMMAND             CREATED             STATUS              PORTS               NAMES
2533adf280ac        schoolofdevops/loop   "program"           6 minutes ago       Up 6 minutes                            prickly_bose
```

## Creating and Starting a Container instead of Running  
Docker **run** command will create a container and start that container simultaneously. However Docker gives you the granularity to create a container and not to run it at the time of creation. However, This container can be started by using **start** command

[Command]  
```
docker create alpine:3.4 sh
```

Run **docker ps -l** to see the status of the container

[Output]  
```
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
22146d15eb71        alpine:3.4          "sh"                31 seconds ago      Created                                 grave_leavitt
```

If you do **docker ps -l**, you will find that container status to be **Created**. Now lets start this container by executing,

[Command]  
```
docker start 22146d15eb71
```

Run docker ps -l again to see the status change

[Output]  
```
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                     PORTS               NAMES
22146d15eb71        alpine:3.4          "sh"                3 minutes ago       Exited (0) 2 minutes ago                      grave_leavitt
```

This command will start the container and exit right away we have not specified interactive mode in the command

## Creating Pretty Reports with Formatters  
The following command will print the output in a way that we desire

```
docker ps --format "{{.ID}}: {{.Status}}"
```

[Output]  
```
2533adf280ac: Up 12 minutes
```

## Stopping and Removing Containers  
We have learnt about interacting with a container, running a container, pausing and unpausing a container, creating and starting a container. But what if you want to stop the container or remove the container itself

### Stop a container  
A container can be stopped using **stop** command. This command will stop the application inside that container hence the container itself will be stopped. This command basically sends a **SIGTERM** signal to the container (graceful shutdown)

[Command]  
```
docker stop 2533adf280ac
```

[Output]  
```
2533adf280ac
```

### Kill a container  
This command will send **SIGKILL** signal and kills the container ungracefully

[Command]  
```
docker kill 590e7060743a
```

[Output]  
```
590e7060743a
```

If you want to remove a container, then execute the following command. Before running this command, run docker ps -a to see the list of pre run containers. Choose a container of your wish and then execute docker rm command. Then run docker ps -a again to check the removed container list or not

[Command]  
```
docker rm 590e7060743a
```

[Output]  
```
590e7060743a
```
# Managing Containers - Learning about Common Container Operations

In the previous chapter, we have learnt about container lifecycle management including how to create, launch, connect to, stop and remove containers. In this chapter, we are going to learn how to launch a container with a pre built app image and how to access the app with published ports. We will also learn about common container operations such as inspecting container information, checking logs and performance stats, renaming and updating the properties of a container, limiting resources etc.  

As part of the tutorial, we are going to setup a shiny new blogging/publishing site. To set it up, we will use a node.js based framework called **ghost**, a simple, fast, and SEO friendly alternative to more sophisticated publishing platforms such as wordpress. However, its purely gives us a blogging platform.  

### Launching a container with a pre built app image  

To launch ghost container run the following command. Don't bother about the new flag **-P** now. We will explain about that flag later in this chapter  
```
docker run -itd -P ghost:0.10.1
```  
[Output]  

```
Unable to find image 'ghost:0.10.1' locally
0.10.1: Pulling from library/ghost

8ad8b3f87b37: Pull complete
751fe39c4d34: Pull complete
3c8031bea3fa: Pull complete
854b52827bb4: Pull complete
f2c2db6ff75a: Pull complete
8e874614dce5: Pull complete
3aa1c5caad55: Pull complete
0cb1edc0454a: Pull complete
6d8ba59589a6: Pull complete
bff20c590458: Pull complete
Digest: sha256:2258f67d3cc513dbf205d5e793e6a9d7359ba28cf16fc5dce08b4e5d2b982245
Status: Downloaded newer image for ghost:0.10.1
3e3b4f0b54dc6d24ee95f24dcbd6472fce541568e1fbb56c982913ca4cb58e15
```
Lets check the status of the container  
```
docker ps
```  
[Output]  

```
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                     NAMES
3e3b4f0b54dc        ghost:0.10.1        "/entrypoint.sh npm s"   7 seconds ago       Up 5 seconds        0.0.0.0:32768->2368/tcp  hungry_lalande
```  

### Renaming the container  
We can rename the container by using following command  
```
docker rename hungry_lalande ghost
```  
We have changed container's automatically generated name to ghost. This new name can be of your choice. The point to understand is this command takes two arguments. The **Old_name followed by New_name**
Run docker ps command to check the effect of changes  
```
docker ps
```  
[Output]  

```
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                     NAMES
3e3b4f0b54dc        ghost:0.10.1        "/entrypoint.sh npm s"   12 minutes ago      Up 12 minutes       0.0.0.0:32768->2368/tcp   ghost
```  
As you can see here, the container is renamed to **ghost**. This makes referencing container in cli very much easier.  

### Ready to experience Ghost?  
Let's see what this **ghost** application does by connecting to that application. For that we need,  
  * Host machine's IP  
  * Container's port which is mapped to a host's port
To find out host machine's IP, we will use **docker machine**. More about this docker orchestration utility will be explained later in the book. The same can be achieved by running a simple ifconfig command in the host machine. But if you understand what docker machine command can do from the starting itself, it will benefit you to understand about this utility quite easily  

```
docker-machine ip default
```  

**TODO:Command is not working - Host does not exist **  

Let's find out the port mapping of container to host. Docker provides subcommand called **port** which does this job  

```
docker port ghost  
```  
[Output]  

```
2368/tcp -> 0.0.0.0:32768
```  
So whatever traffic the host gets in port **2368** will be mapped to container's port **32768**  

Let's connect to http://IP_ADDRESS:PORT to see the actual application  

![ghost-welcome](images/ghost-welcome.png)

### Configure blog and add some content  
Let us set up ghost now. Let log into admin console of ghost by visiting following URL  
```
http://HOST:PORT/ghost
```  
Now follow these instructions  
![setup](images/setup-1.png)  
![setup](images/setup-2.png)  
![setup](images/setup-3.png)  
![setup](images/setup-4.png)  
![setup](images/setup-5.png)  

There you go. Now you have successfully published an article on ghost  
Visit the homepage again to see it  

### Finding Everything about the running  container
This topic discusses about finding metadata of containers. These metadata include various parameters like,  
  * State of the container  
  * Mounts  
  * Configuration  
  * Network, etc.,  

#### Inspecting
Lets try this inspect subcommand in action  

```
docker inspect ghost
```  

[Output]  

```
[
    {
        "Id": "3e3b4f0b54dc6d24ee95f24dcbd6472fce541568e1fbb56c982913ca4cb58e15",
        "Created": "2016-09-15T14:07:10.939365783Z",
        "Path": "/entrypoint.sh",
        "Args": [
            "npm",
            "start"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 6219,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2016-09-15T14:07:11.903893634Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:b73bd21ec0477e02c853b6b086a67d96af56fd62e0fa3d81b17893fa923d9873",
        "ResolvConfPath": "/var/lib/docker/containers/3e3b4f0b54dc6d24ee95f24dcbd6472fce541568e1fbb56c982913ca4cb58e15/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/3e3b4f0b54dc6d24ee95f24dcbd6472fce541568e1fbb56c982913ca4cb58e15/hostname",
        "HostsPath": "/var/lib/docker/containers/3e3b4f0b54dc6d24ee95f24dcbd6472fce541568e1fbb56c982913ca4cb58e15/hosts",
        "LogPath": "/var/lib/docker/containers/3e3b4f0b54dc6d24ee95f24dcbd6472fce541568e1fbb56c982913ca4cb58e15/3e3b4f0b54dc6d24ee95f24dcbd6472fce            541568e1fbb56c982913ca4cb58e15-json.log",
        "Name": "/ghost",
        "RestartCount": 0,
        "Driver": "devicemapper",
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
            "PortBindings": {},
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
            "IpcMode": "",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": true,
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
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": null,
            "BlkioDeviceReadBps": null,
            "BlkioDeviceWriteBps": null,
            "BlkioDeviceReadIOps": null,
            "BlkioDeviceWriteIOps": null,
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DiskQuota": 0,
            "KernelMemory": 0,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": -1,
            "OomKillDisable": false,
            "PidsLimit": 0,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0
        },
        "GraphDriver": {
            "Name": "devicemapper",
            "Data": {
                "DeviceId": "23",
                "DeviceName": "docker-253:0-67238294-fcd6f0f0c695b522cc7939f10eb29edd993a348b25573b5f40a4d59bb459f77c",
                "DeviceSize": "10737418240"
            }
        },
        "Mounts": [
            {
                "Name": "d7cdbdaa5b140554769a38d0c77b91720c6e687c5f2f471f03b5b89cd351cf56",
                "Source": "/var/lib/docker/volumes/d7cdbdaa5b140554769a38d0c77b91720c6e687c5f2f471f03b5b89cd351cf56/_data",
                "Destination": "/var/lib/ghost",
                "Driver": "local",
                "Mode": "",
                "RW": true,
                "Propagation": ""
            }
        ],
        "Config": {
            "Hostname": "3e3b4f0b54dc",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "2368/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "NPM_CONFIG_LOGLEVEL=info",
                "NODE_VERSION=4.5.0",
                "GOSU_VERSION=1.7",
                "GHOST_SOURCE=/usr/src/ghost",
                "GHOST_VERSION=0.10.1",
                "GHOST_CONTENT=/var/lib/ghost"
            ],
            "Cmd": [
                "npm",
                "start"
            ],
            "Image": "ghost:0.10.1",
            "Volumes": {
                "/var/lib/ghost": {}
            },
            "WorkingDir": "/usr/src/ghost",
            "Entrypoint": [
                "/entrypoint.sh"
            ],
            "OnBuild": null,
            "Labels": {}
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "434d8142bfbbd63f45c31a18ee2cb9e24b22afad93c964da69de556d531b89dd",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {
                "2368/tcp": [
                    {
                        "HostIp": "0.0.0.0",
                        "HostPort": "32768"
                    }
                ]
            },
            "SandboxKey": "/var/run/docker/netns/434d8142bfbb",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "1905f7756420f7c4361478b55291d2157f9a5e6a48338b1a6133cef76b45a5a4",
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
                    "NetworkID": "e4b05962c438ad0741bacd05493668c856d837b4615257136d2ce037f81ce42b",
                    "EndpointID": "1905f7756420f7c4361478b55291d2157f9a5e6a48338b1a6133cef76b45a5a4",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.2",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:02"
                }
            }
        }
    }
]

```  
This data is represented in JSON format which makes filtering these results easier.  

#### Checking the Stats  
##### Stats command  
This command returns a data stream of resource utilization used by containers. The flag **--no-stream** disables data stream and displays only first result  

```
docker stats --no-stream=true ghost
```  

[Output]  

```
CONTAINER           CPU %               MEM USAGE / LIMIT       MEM %               NET I/O               BLOCK I/O           PIDS
ghost               0.00%               214.8 MiB / 1.797 GiB   11.67%              146.6 kB / 2.168 MB   0 B / 4.375 MB      0

```  

##### Top command  
To display the list of processes and the information about those processes that are running inside the container, we can use **top** command

```
docker top ghost
```  

[Output]  

```
UID                 PID                 PPID                C                   STIME               TTY                 TIME                CMD
vagrant             6219                6211                0                   14:07               ?                   00:00:00            npm
vagrant             6275                6219                0                   14:07               ?                   00:00:00            sh -c node index
vagrant             6276                6275                0                   14:07               ?                   00:00:11            node index

```

### Examine Logs  
Docker **log** command is to print the logs of the application inside the container. In our case we will see the log output of ghost application  

```
docker logs ghost
```  

[Output]  

```
POST /ghost/api/v0.1/posts/?include=tags 422 165.523 ms - 120
GET /ghost/api/v0.1/posts/?page=1&limit=15&status=all&staticPages=all&include=tags 200 66.134 ms - -
GET /ghost/api/v0.1/slugs/post/(Untitled)/ 200 43.748 ms - 31
POST /ghost/api/v0.1/posts/?include=tags 201 73.500 ms - 479
PUT /ghost/api/v0.1/posts/2/?include=tags 200 107.108 ms - 479
PUT /ghost/api/v0.1/posts/2/?include=tags 200 261.262 ms - 607
PUT /ghost/api/v0.1/posts/2/?include=tags 200 92.373 ms - 740
PUT /ghost/api/v0.1/posts/2/?include=tags 200 197.701 ms - 742
PUT /ghost/api/v0.1/posts/2/?include=tags 200 109.857 ms - -
PUT /ghost/api/v0.1/posts/2/?include=tags 200 239.978 ms - 742
PUT /ghost/api/v0.1/posts/2/?include=tags 200 176.895 ms - -
PUT /ghost/api/v0.1/posts/2/?include=tags 200 80.514 ms - -
PUT /ghost/api/v0.1/posts/2/?include=tags 200 127.901 ms - -
PUT /ghost/api/v0.1/posts/2/?include=tags 200 279.284 ms - -
GET /ghost/api/v0.1/posts/?page=1&limit=15&status=all&staticPages=all&include=tags 200 78.747 ms - -
GET /ghost/api/v0.1/posts/?page=1&limit=15&status=all&staticPages=all&include=tags 200 131.023 ms - -
GET /ghost/api/v0.1/posts/2/?status=all&staticPages=all&include=tags 200 76.145 ms - -
PUT /ghost/api/v0.1/posts/2/?include=tags 200 219.867 ms - -
DELETE /ghost/api/v0.1/posts/2/ 204 139.318 ms - -
GET /ghost/api/v0.1/posts/?page=1&limit=15&status=all&staticPages=all&include=tags 200 68.736 ms - -
GET /ghost/api/v0.1/slugs/post/(Untitled)/ 200 110.837 ms - 31
POST /ghost/api/v0.1/posts/?include=tags 201 119.802 ms - 479
PUT /ghost/api/v0.1/posts/3/?include=tags 200 90.819 ms - -
PUT /ghost/api/v0.1/posts/3/?include=tags 200 144.269 ms - -
PUT /ghost/api/v0.1/posts/3/?include=tags 200 207.297 ms - -
GET / 200 102.683 ms - -
GET /ghost/editor/3/ 200 101.009 ms - -
GET /ghost/api/v0.1/settings/?type=blog%2Ctheme%2Cprivate 200 35.038 ms - -
GET /ghost/api/v0.1/users/me/?include=roles&status=all 200 39.853 ms - 726
GET /ghost/api/v0.1/notifications/ 200 30.542 ms - 20
GET /ghost/api/v0.1/posts/3/?status=all&staticPages=all&include=tags 200 39.482 ms - -
GET /ghost/api/v0.1/settings/?type=blog%2Ctheme%2Cprivate 200 21.556 ms - -
GET /ghost/api/v0.1/tags/?limit=all 200 52.398 ms - 426
GET /ghost/api/v0.1/users/?limit=all&include=roles 200 53.609 ms - 817
PUT /ghost/api/v0.1/posts/3/?include=tags 200 81.172 ms - -
PUT /ghost/api/v0.1/posts/3/?include=tags 200 228.299 ms - -
GET / 200 139.860 ms - -

```  

If you want to **follow** the log in real-time, use **-f** flag  

```
docker logs -f ghost
```  

[Output]  

```
POST /ghost/api/v0.1/posts/?include=tags 422 165.523 ms - 120
GET /ghost/api/v0.1/posts/?page=1&limit=15&status=all&staticPages=all&include=tags 200 66.134 ms - -
GET /ghost/api/v0.1/slugs/post/(Untitled)/ 200 43.748 ms - 31
POST /ghost/api/v0.1/posts/?include=tags 201 73.500 ms - 479
PUT /ghost/api/v0.1/posts/2/?include=tags 200 107.108 ms - 479
PUT /ghost/api/v0.1/posts/2/?include=tags 200 261.262 ms - 607
PUT /ghost/api/v0.1/posts/2/?include=tags 200 92.373 ms - 740
PUT /ghost/api/v0.1/posts/2/?include=tags 200 197.701 ms - 742
PUT /ghost/api/v0.1/posts/2/?include=tags 200 109.857 ms - -
PUT /ghost/api/v0.1/posts/2/?include=tags 200 239.978 ms - 742
PUT /ghost/api/v0.1/posts/2/?include=tags 200 176.895 ms - -
PUT /ghost/api/v0.1/posts/2/?include=tags 200 80.514 ms - -
PUT /ghost/api/v0.1/posts/2/?include=tags 200 127.901 ms - -
PUT /ghost/api/v0.1/posts/2/?include=tags 200 279.284 ms - -
GET /ghost/api/v0.1/posts/?page=1&limit=15&status=all&staticPages=all&include=tags 200 78.747 ms - -
GET /ghost/api/v0.1/posts/?page=1&limit=15&status=all&staticPages=all&include=tags 200 131.023 ms - -
GET /ghost/api/v0.1/posts/2/?status=all&staticPages=all&include=tags 200 76.145 ms - -
PUT /ghost/api/v0.1/posts/2/?include=tags 200 219.867 ms - -
DELETE /ghost/api/v0.1/posts/2/ 204 139.318 ms - -
GET /ghost/api/v0.1/posts/?page=1&limit=15&status=all&staticPages=all&include=tags 200 68.736 ms - -
GET /ghost/api/v0.1/slugs/post/(Untitled)/ 200 110.837 ms - 31
POST /ghost/api/v0.1/posts/?include=tags 201 119.802 ms - 479
PUT /ghost/api/v0.1/posts/3/?include=tags 200 90.819 ms - -
PUT /ghost/api/v0.1/posts/3/?include=tags 200 144.269 ms - -
PUT /ghost/api/v0.1/posts/3/?include=tags 200 207.297 ms - -
GET / 200 102.683 ms - -
GET /ghost/editor/3/ 200 101.009 ms - -
GET /ghost/api/v0.1/settings/?type=blog%2Ctheme%2Cprivate 200 35.038 ms - -
GET /ghost/api/v0.1/users/me/?include=roles&status=all 200 39.853 ms - 726
GET /ghost/api/v0.1/notifications/ 200 30.542 ms - 20
GET /ghost/api/v0.1/posts/3/?status=all&staticPages=all&include=tags 200 39.482 ms - -
GET /ghost/api/v0.1/settings/?type=blog%2Ctheme%2Cprivate 200 21.556 ms - -
GET /ghost/api/v0.1/tags/?limit=all 200 52.398 ms - 426
GET /ghost/api/v0.1/users/?limit=all&include=roles 200 53.609 ms - 817
PUT /ghost/api/v0.1/posts/3/?include=tags 200 81.172 ms - -
PUT /ghost/api/v0.1/posts/3/?include=tags 200 228.299 ms - -
GET / 200 139.860 ms - -
GET / 304 67.779 ms - -
GET /assets/css/screen.css?v=5799f9cac6 304 2.539 ms - -
GET /assets/js/jquery.fitvids.js?v=5799f9cac6 304 4.560 ms - -
GET /assets/js/index.js?v=5799f9cac6 304 3.353 ms - -
GET /assets/fonts/casper-icons.woff?v=1 304 0.889 ms - -
GET /favicon.ico 200 0.134 ms - -
GET /hi-there/ 200 131.892 ms - -

```  
Now try to read the articles available in our blog and see the log output gets updated in real-time. Hit **ctrl+c** to break the stream  

### Stream events from a container  
Docker **events** serves us with the stream of events or interactions that are happening with the docker daemon. This does not stream the log data of application inside the container. That is done by **docker logs** command. Let us see how this command works  
Open an another terminal *(git bash)* from *vagrant parent directory* and ssh into your Docker host. Now you should have two terminals for  the same machine **(Docker host)**. Let us call the old terminal as **Terminal 1** and the newer one as **Terminal 2**.

From Terminal 1, execute **docker events**. Now you are getting the data stream from docker daemon  

```
docker events
```  

To understand how this command actually works, let us run a container from Terminal 2  

```
docker run -ti alpine:3.4 sh  
```  

If you see, in Terminal 1, the interaction with docker daemon, while running that container will be printed  

[Output - **Terminal 1**]  

```
2016-09-16T13:00:20.189028004Z container create 816fcc5e9c8dca13c76f3ff4546a7769bed497c4f4153b20ec34459c88f7b923 (image=alpine:3.4, name=tiny_franklin)
2016-09-16T13:00:20.190190470Z container attach 816fcc5e9c8dca13c76f3ff4546a7769bed497c4f4153b20ec34459c88f7b923 (image=alpine:3.4, name=tiny_franklin)
2016-09-16T13:00:20.257068692Z network connect c0237b5406920749b87460597b8935adf958bae1ce997afd827921a0dbc97cdc (container=816fcc5e9c8dca13c76f3ff4546a7769bed497c4f4153b20ec34459c88f7b923, name=bridge, type=bridge)
2016-09-16T13:00:20.346533821Z container start 816fcc5e9c8dca13c76f3ff4546a7769bed497c4f4153b20ec34459c88f7b923 (image=alpine:3.4, name=tiny_franklin)
2016-09-16T13:00:20.347811877Z container resize 816fcc5e9c8dca13c76f3ff4546a7769bed497c4f4153b20ec34459c88f7b923 (height=41, image=alpine:3.4, name=tiny_franklin, width=126)
```  

Try to do various docker operations (start, stop, rm, etc.,) and see the output in Terminal 1  

### Attach to the container  
Normally, when we run a container, we use **-d** flag to run that container in detached mode. But sometimes you might require to make some changes inside that container. In those kind of situations, we can use **attach** command. This command attaches to the tty of docker container. So it will stream the output of the application. In our case, we will see the output of ghost application  

```
docker attach ghost
```  
Hit our blogs url several times to see the output  

[Output]  

```
POST /ghost/api/v0.1/authentication/token 200 418.439 ms - -
GET /ghost/api/v0.1/settings/?type=blog%2Ctheme%2Cprivate 200 69.950 ms - -
GET /ghost/img/invite-placeholder.png 200 1.279 ms - 7860
GET /ghost/img/users.png 200 4.739 ms - 49253
GET /ghost/api/v0.1/users/me/?include=roles&status=all 200 64.548 ms - 726
GET /ghost/api/v0.1/notifications/ 200 43.159 ms - 513
GET /ghost/api/v0.1/posts/?page=1&limit=15&status=all&staticPages=all&include=tags 200 61.997 ms - -
GET /ghost/img/ghosticon.jpg 200 2.592 ms - 2499

```  

You can detach from the tty by pressing **ctrl-p + ctrl-q** in sequence. If you haven't started your container with ** -itd ** flag, then it is not possible to get your host's terminal back. In that case, If you haven't started the container with **-itd** option, then you have to use **--sig-proxy=false** falg with the attach command.  Then you will be able to detach from the container by using **ctrl-c**  
It is possible to override these keys too. For that we have to add --detach-keys flag to the command. To learn more, click on the following URL  

https://docs.docker.com/engine/reference/commandline/attach/  

### Copying files between container and client host  

We can copy files/directories form host to container and vice-versa    
Let us create a file on the host  
```
touch testfile
```  

To copy the testfile **from host machine to ghsot contanier**, try  
```
docker cp testfile ghost:/opt  
```  
This command will copy testfile to ghost container's **/opt** directory  and will not give any output. To verify the file has been copies or not, let us log into container by running,  

```
docker exec -it ghost bash
```  
Change directory into /opt and list the files  

```
cd /opt  
ls
```  

[Output]  

```
testfile
```  

There you can see that file has been successfully copied. Now exit the container  

Now you may try to cp some files **from the container to the host machine**  
Before that you have to change host machine's current working directory to **/vagrant**. This has to be done, because the CentOS VM is **mounted** that directory only.  

```
cd /vagrant  
docker cp ghost:/usr/src/ghost .  
ls  
```  
You might get some protocol errors. The reason for this is, it tries to create a symlink to a file on host machine, which does not exist.  

### Rename a  container  
When you want to rename a container, we can use use **rename** command. Let us change our **ghost** container's name to **ghostapp**. Try *docker ps* to see the changes,

 ```
 docker rename ghost ghostapp  
 docker ps  
 ```  

 [Output]  

 ```
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                     NAMES
b28efeef41f8        ghost:0.10.1        "/entrypoint.sh npm s"   20 hours ago        Up 2 minutes        0.0.0.0:32768->2368/tcp   ghostapp
 ```

### Controlling Resources  
Docker provides us the granularity to control each container's **resource utilization**. We have several commands in the inventory to achieve this  

#### Putting limits on Running Containers  
First, let us see the memory utilization of our ghostapp container, by trying

```
docker inspect ghostapp | grep -i memory  
```  

[Output]  

```
"Memory": 0,
"KernelMemory": 0,
"MemoryReservation": 0,
"MemorySwap": 0,
"MemorySwappiness": -1,
```  

You can see that **Memory** attribute has **0** as its value. 0 means unlimited usage of host's RAM. We can put a cap on that by using **update** command  

```
docker update -m 400M ghostapp  
```  

[Output]  

```
ghostapp
```  
Let us check whether the change has taken effect or not  

```
docker inspect ghostapp | grep -i memory
```  

[Output]  

```
"Memory": 419430400,
"KernelMemory": 0,
"MemoryReservation": 0,
"MemorySwap": 0,
"MemorySwappiness": -1,

```  
As you can see, the memory utilization of the container is changed from 0 (unlimited) to 400 mb  

#### Limiting Resources while launching new containers  
The following resources can be limited using the *update* command  
  * CPU
  * Memory
  * Disk IO
  * Capabilities  

Open two terminals, lets call them T1, and T2  
In T1, start monitoring the stats  

```
docker stats
```  

[Output]  
```
CONTAINER           CPU %               MEM USAGE / LIMIT     MM %               NET I/O             BLOCK I/O             PIDS
b28efeef41f8        0.16%               190.1 MiB / 400 MiB   47.51%              1.296 kB / 648 B    86.02 kB / 45.06 kB   0
CONTAINER           CPU %               MEM USAGE / LIMIT     MEM %               NET I/O             BLOCK I/O             PIDS
b28efeef41f8        0.01%               190.1 MiB / 400 MiB   47.51%              1.296 kB / 648 B    86.02 kB / 45.06 kB   0
```

From T2, launch two containers with different CPU shares. Default CPU shares are set to 1024. This is a relative weight.  

```
docker run -d --name st-01  schoolofdevops/stresstest stress --cpu 1

docker run -d --name st-02 -c 512  schoolofdevops/stresstest stress --cpu 1

```  
When you launch the first container, it will use the full quota of CPU, i.e., 100%  

[Output - **After first container launch**]  

```
CONTAINER           CPU %               MEM USAGE / LIMIT       MEM %               NET I/O             BLOCK I/O             PIDS
b28efeef41f8        0.01%               190.1 MiB / 400 MiB     47.51%              1.944 kB / 648 B    86.02 kB / 45.06 kB   0
764f158d6523        102.73%             2.945 MiB / 1.797 GiB   0.16%               648 B / 648 B       3.118 MB / 0 B        0
```  

[Output - **After second container lauch**]  

```
CONTAINER           CPU %               MEM USAGE / LIMIT       MEM %               NET I/O             BLOCK I/O             PIDS
b28efeef41f8        0.00%               190.1 MiB / 400 MiB     47.51%              2.592 kB / 648 B    86.02 kB / 45.06 kB   0
764f158d6523        66.97%              2.945 MiB / 1.797 GiB   0.16%               1.296 kB / 648 B    3.118 MB / 0 B        0
a13f98995ade        33.36%              2.945 MiB / 1.797 GiB   0.16%               648 B / 648 B       3.118 MB / 0 B        0
```  

Observe stats in T1
Launch a couple more nodes with different cpu shares, observe how T2 stats change  

```
docker run -d --name st-03 -c 512  schoolofdevops/stresstest stress --cpu 1

docker run -d --name st-04  schoolofdevops/stresstest stress --cpu 1

```  

[Output - **After all containers are launched**]  

```
CONTAINER           CPU %               MEM USAGE / LIMIT       MEM %               NET I/O             BLOCK I/O             PIDS
b28efeef41f8        0.00%               190.1 MiB / 400 MiB     47.51%              3.888 kB / 648 B    86.02 kB / 45.06 kB   0
764f158d6523        32.09%              2.945 MiB / 1.797 GiB   0.16%               2.592 kB / 648 B    3.118 MB / 0 B        0
a13f98995ade        16.02%              2.945 MiB / 1.797 GiB   0.16%               1.944 kB / 648 B    3.118 MB / 0 B        0
f04e9ea5627c        16.37%              2.949 MiB / 1.797 GiB   0.16%               1.296 kB / 648 B    3.118 MB / 0 B        0
abeab389a873        31.71%              2.949 MiB / 1.797 GiB   0.16%               648 B / 648 B       3.118 MB / 0 B        0
```  
Close the T2 terminal  

#### Exercises  
Try to these exercises, to get a better understanding  
  * Put a memory limit
  * Set disk iops

### Launching Containers with Elevated  Privileges  
When the operator executes docker run --privileged, Docker will enable to access to all devices on the host as well as set some configuration in AppArmor or SELinux to allow the container nearly all the same access to the host as processes running outside containers on the host.

#### Example:  
##### Running a sysdig container to monitor docker  
Sysdig tool allows us to monitor the processes that are going on in the other containers. It is more like running a top command from one container on behalf of others.  

```
docker run -itd --name=sysdig --privileged=true \
           --volume=/var/run/docker.sock:/host/var/run/docker.sock \
           --volume=/dev:/host/dev \
           --volume=/proc:/host/proc:ro \
           --volume=/boot:/host/boot:ro \
           --volume=/lib/modules:/host/lib/modules:ro \
           --volume=/usr:/host/usr:ro \
           sysdig/sysdig:0.11.0 sysdig
```  
[Output]  
```
Unable to find image 'sysdig/sysdig:0.11.0' locally
0.11.0: Pulling from sysdig/sysdig

0f409b0f5b3d: Pull complete
64965da77fc6: Pull complete
588eeb0d4c30: Pull complete
9aa18e35b362: Pull complete
cc036f2dca14: Pull complete
33400f3af946: Pull complete
b39ed90e36fd: Pull complete
1fca16436380: Pull complete
Digest: sha256:ee9d66a07308c5aef91f070cce5c9fb891e4fefb5da4d417e590662e34846664
Status: Downloaded newer image for sysdig/sysdig:0.11.0
6ba17cf2af7b87621b3380517af45c5785dc8cda75111f0f8c36bb83e163a120
```

```
docker exec -it sysdig bash
csysdig
```  

[Output]  

![sysdig](images/sysdig.png)  

After this, press f2 and select **containers** tab  
Now check what are the processes are running in other containers  

![sysdig](images/sysdig2.png)  


##### References

[Resource Management in Docker by Marek Goldmann] (https://goldmann.pl/blog/2014/09/11/resource-management-in-docker/)

# Dockerizing your Applications : Building Images and Working with Registries

In the previous session, we have learnt about various container operations such as running containers from
pre built images, port mapping, inspecting and updating containers, limiting resources etc., In this
chapter, we are going to learn about how to build containers for your individual applications, as well
as how to work with docker hub registry to host and distribute the images.  


### Registering with the Registry : Creating an Account on DockerHub
Since we are going to start working with the registry, build and push images to it later, its essential to have our own account on the registry. For the purpose of this tutorial, we are going to use the hosted registry i.e. Dockerhub.  

Steps to create Dockerhub account  
#### Step 1:  
Visit the following link and sign up with your email id  
  **https://hub.docker.com/**

  ![hub](images/chp6/hub1.png)  

#### Step 2:  
Check your email inbox and check the activation email sent by docker team  

#### Step 3:  
After clicking on the activation link, you will be redirected to a log in page. Enter your credentials and log in  

  ![hub](images/chp6/hub2.png)  

You will be launched to Dockerhub main page. Now the registration process is complete and you have account in Dockerhub!  

  ![hub](images/chp6/hub3.png)  

### Building Docker Images - A manual approach

Before we start building automated images, we are going to create a docker image by hand. We have already used the pre built image from the registry in the last session. In this session, however, we are going to create our own image with ghost installed. Since Ghost is a node.js based application, we will base our work on existing offical image for **node**  

##### Types of Images  

  * Slim  
  * Complete  

To search an image from the registry we could use,  

```
docker search node
```  

[Output]  

```
NAME                      DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
node                      Node.js is a JavaScript-based platform for...   2815      [OK]
strongloop/node           StrongLoop, Node.js, and tools.                 31                   [OK]
nodered/node-red-docker   Node-RED Docker images.                         24                   [OK]
bitnami/node              Bitnami Node.js Docker Image                    16                   [OK]
siomiz/node-opencv        _/node + node-opencv                            8                    [OK]
calico/node                                                               8                    [OK]
dahlb/alpine-node         small node for gitlab ci runner                 7                    [OK]
cusspvz/node              🌐 Super small Node.js container (~15MB)...      5                    [OK]
anigeo/node-forever       Daily build node.js with forever                4                    [OK]
azukiapp/node             Docker image to run Node.js by Azuki - htt...   4                    [OK]
tutum/node                Run a Tutum node inside a container             3                    [OK]
seegno/node               A node docker base image.                       2                    [OK]
starefossen/ruby-node     Docker Image with Ruby and Node.js installed    2                    [OK]
wallarm/node              Wallarm Node                                    2                    [OK]
urbanmassage/node         Some handy (read, better) docker node images    1                    [OK]
joxit/node                Slim node docker with some utils for dev        1                    [OK]
tectoro/node-compass      Node JS minimal version with compass and b...   1                    [OK]
centralping/node          Bare bones CentOS 7 NodeJS container.           1                    [OK]
redjack/node              Node + Nave                                     1                    [OK]
xataz/node                very light node image                           1                    [OK]
robbertkl/node            Docker container running Node.js                0                    [OK]
instructure/node          Instructure node images                         0                    [OK]
c4tech/node               NodeJS images, aimed at generated single-p...   0                    [OK]
codexsystems/node         Node.js for Development and Production          0                    [OK]
watsco/node               node:6                                          0                    [OK]

```

You could find the same results when you search using the UI

TODO: Add a screenshot which shows searching for node image on docker hub

Lets launch a intermediate container using the image above. We will use this container to install and configure ghost and its dependencies.  

```
docker run -idt --name intermediate node:4-slim bash
```

[Output]  

```   
  Unable to find image 'node:4-slim' locally
  4-slim: Pulling from library/node

  8ad8b3f87b37: Pull complete
  751fe39c4d34: Pull complete
  3c8031bea3fa: Pull complete
  854b52827bb4: Pull complete
  Digest: sha256:52d18a901cf295f5035cc98ad23473ee3f0acffa2f49683e921cf27c343ae774
  Status: Downloaded newer image for node:4-slim
  root@5a9d73b026e8:/#
```  

```
docker ps  
```  

[Output]  

```  
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
5e8153390e17        node:4-slim         "bash"              7 seconds ago       Up 5 seconds                            intermediate
```  

```
docker exec -it intermediate bash
```  

[Output]  

```
docker exec -it intermediate bash
root@5e8153390e17:/#
```  

##### Install and Configure Ghost on a Debian/Ubuntu system  

Install pre-requisites  

```
apt-get update && apt-get install -y gcc make python unzip vim

```  

Download and install ghost  

```  
mkdir /usr/src/ghost
cd /usr/src/ghost/
wget -c https://ghost.org/archives/ghost-0.10.1.zip  

```  

[Output]  

```
wget -c https://ghost.org/archives/ghost-0.10.1.zip
converted 'https://ghost.org/archives/ghost-0.10.1.zip' (ANSI_X3.4-1968) -> 'https://ghost.org/archives/ghost-0.10.1.zip' (UTF-8)
--2016-09-18 17:20:16--  https://ghost.org/archives/ghost-0.10.1.zip
Resolving ghost.org (ghost.org)... 104.16.83.186, 104.16.85.186, 104.16.81.186, ...
Connecting to ghost.org (ghost.org)|104.16.83.186|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 3988064 (3.8M) [application/zip]
Saving to: 'ghost-0.10.1.zip'

ghost-0.10.1.zip                           100%[========================================================================================>]   3.80M  30.9KB/s   in 2m 12s

2016-09-18 17:22:34 (29.5 KB/s) - 'ghost-0.10.1.zip' saved [3988064/3988064]
```  

```
unzip ghost-0.10.1.zip  
```  

[Output]  

```
Archive:  ghost-0.10.1.zip
  inflating: config.example.js
   creating: content/
   creating: content/apps/
  inflating: content/apps/README.md
   creating: content/data/
  inflating: content/data/README.md
   creating: content/images/
  inflating: content/images/README.md
   creating: content/themes/
   creating: content/themes/casper/
   creating: content/themes/casper/assets/
   creating: content/themes/casper/assets/css/
  inflating: content/themes/casper/assets/css/screen.css
   creating: content/themes/casper/assets/fonts/
  inflating: content/themes/casper/assets/fonts/casper-icons.eot
  inflating: content/themes/casper/assets/fonts/casper-icons.svg
  inflating: content/themes/casper/assets/fonts/casper-icons.ttf
  inflating: content/themes/casper/assets/fonts/casper-icons.woff
   creating: content/themes/casper/assets/js/
```  

```  
npm install --production
```  

[Output]  

```
npm info installOne string_decoder@0.10.31
npm info installOne core-util-is@1.0.2
npm info postinstall fs.realpath@1.0.0
npm info install boolbase@1.0.0 into /usr/src/ghost/node_modules/cheerio/node_modules/css-select
npm info install css-what@2.1.0 into /usr/src/ghost/node_modules/cheerio/node_modules/css-select
npm info install nth-check@1.0.1 into /usr/src/ghost/node_modules/cheerio/node_modules/css-select
npm info install domutils@1.5.1 into /usr/src/ghost/node_modules/cheerio/node_modules/css-select
npm info installOne boolbase@1.0.0
npm info installOne css-what@2.1.0
npm info installOne nth-check@1.0.1
npm info installOne domutils@1.5.1

```  
Create configuration for ghost  

```
cd /usr/src/ghost; mv config.example.js config.js  

```  

Edit config.js  

```
vim config.js

```  

Scroll to development block and change the server config to use 0.0.0.0 instead of 127.0.0.1  
E.g.  
```
            host: '0.0.0.0',
```

Cleanup  

```
apt-get purge -y --auto-remove gcc make python unzip vim
rm -rf /var/lib/apt/lists/*
rm ghost-0.10.1.zip
npm cache clean

```

[Output]  

```
npm info it worked if it ends with ok
npm info using npm@2.15.9
npm info using node@v4.5.0
npm info ok

```

```
rm -rf /tmp/npm*

```  

Exit from the container.  

Note down the container id for the container you just modified and exited from.  

```
docker ps -l

```

[Output]  

```
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
ea2d0ac8476e        node:4-slim         "bash"              50 minutes ago      Up 50 minutes                           intermediate
```  

To create a image by taking a snasnapshot of the container use the following command,

```
docker commit -a "Firstname Lastname" -m "commit message" CONTAINER HUB_USERNAME/REPO:TAG  

E.g. docker commit -a "John Doe" -m "creating custom ghost image" c082972f66d6 mydockerhubid/ghost:0.1.0

```  

[Output]  

```
docker commit -a "John Doe" -m "committing the changes" ea2d0ac8476e johmdoe/ghost:0.1.0
sha256:b514e85c275ea6a864987f9a055b3bca817f763868c6c168589179c42cee580c
```  

To launch a container with the above images in a development mode, use


```
docker run -d -w /usr/src/ghost  -p 2368 mydockerhubid/ghost:0.1.0 npm start

```  

[Output]  

```
docker run -d -w /usr/src/ghost  -p 2368 venkatsudharsanam/ghost:0.1.0 npm start
34f4da3403d81329855a52c13ecb0e49a0eee257800be83ddc7dfda569095469
```

Find out the port mapping, connect to http://host:port and validate your image.


### Dockerfiles - Automating Image Builds

Earlier, we created image by launching a intermediate container and manually installing and configuring ghost app. This time we are going to use a Dockerfile, write the specification to build image, and use it to automate the process of building image.  


#### Setting up a ghostapp repo on github  

We are going to setup a git repository where we create the configurations to automate the build process of our image. Later in this chapter, we will also integrate it with Dockerhub to create automated builds. For this purpose, its essential to have a github account.  

  * Create and Account on github, if you do not already have it  
  * Fork the ghostapp repo  
    **https://github.com/schoolofdevops/ghostapp**  
  * Clone the forked repo  
Install git on VM first  
```
yum install git  
```  
Clone the repository  
```
git clone https://github.com/YOUR_GITHUB_ID/ghostapp.git
```  

[Output]  

```
Cloning into 'ghostapp'...
remote: Counting objects: 12, done.
remote: Compressing objects: 100% (9/9), done.
remote: Total 12 (delta 3), reused 12 (delta 3), pack-reused 0
Unpacking objects: 100% (12/12), done.
```  
Change the current working directory  

```  
cd ghostapp
```  

Examine  Dockerfile in ghostapp directory.  

```
ls  
```  

[Output]  

```
config.js  docker-entrypoint.sh  Dockerfile  Dockerfile.inef  install_ghost.sh  LICENSE
```  

#### Building and Image with Dockerfile  
Let us build the docker image from the Dockerfile that we have inside the ghostapp directory  

[Syntax]  

```
docker build -t USERNAME/REPO:TAG  .   
```  
Example:  

```
docker build -t mydockerhubid/ghost:0.2.0 .
```  

Replace mydockerhubid with your DockerHub ID  

[Output]  

```
Sending build context to Docker daemon 79.87 kB
Step 1 : FROM node:4-slim
4-slim: Pulling from library/node

8ad8b3f87b37: Pull complete
751fe39c4d34: Pull complete
3c8031bea3fa: Pull complete
854b52827bb4: Pull complete
Digest: sha256:52d18a901cf295f5035cc98ad23473ee3f0acffa2f49683e921cf27c343ae774
Status: Downloaded newer image for node:4-slim
 ---> 48f7a334e4da
Step 2 : RUN groupadd user && useradd --create-home --home-dir /home/user -g user user
 ---> Running in 0e270a5b9941
 ---> a687627e462e
Removing intermediate container 0e270a5b9941
Step 3 : ENV GOSU_VERSION 1.7
 ---> Running in 9955ac3c391a
 ---> 3f3d9d60c5bb
Removing intermediate container 9955ac3c391a
Step 4 : RUN set -x     && wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$(dpkg --print-architecture)"         && wget -O /usr/local/bin/gosu.asc "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$(dpkg --print-architecture).asc"         && export GNUPGHOME="$(mktemp -d)"      && gpg --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4        && gpg --batch --verify /usr/local/bin/gosu.asc /usr/local/bin/gosu     && rm -r "$GNUPGHOME" /usr/local/bin/gosu.asc   && chmod +x /usr/local/bin/gosu   && gosu nobody true
 ---> Running in e73ed282a080
+ dpkg --print-architecture
+ wget -O /usr/local/bin/gosu https://github.com/tianon/gosu/releases/download/1.7/gosu-amd64
converted 'https://github.com/tianon/gosu/releases/download/1.7/gosu-amd64' (ANSI_X3.4-1968) -> 'https://github.com/tianon/gosu/releases/download/1.7/gosu-amd64' (UTF-8)
--2016-09-18 17:32:22--  https://github.com/tianon/gosu/releases/download/1.7/gosu-amd64
Resolving github.com (github.com)... 192.30.253.112
Connecting to github.com (github.com)|192.30.253.112|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://github-cloud.s3.amazonaws.com/releases/19708981/40d1b00c-8619-11e5-8953-d0122dcf07b9?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAISTNZFOVBIJMK3TQ%2F20160918%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20160918T173223Z&X-Amz-Expires=300&X-Amz-Signature=3f340343a6f1b4d568a1d4ecb2af06c1e766e006ff5ea2c2d354d45c148d163b&X-Amz-SignedHeaders=host&actor_id=0&response-content-disposition=attachment%3B%20filename%3Dgosu-amd64&response-content-type=application%2Foctet-stream [following]
converted 'https://github-cloud.s3.amazonaws.com/releases/19708981/40d1b00c-8619-11e5-8953-d0122dcf07b9?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAISTNZFOVBIJMK3TQ%2F20160918%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20160918T173223Z&X-Amz-Expires=300&X-Amz-Signature=3f340343a6f1b4d568a1d4ecb2af06c1e766e006ff5ea2c2d354d45c148d163b&X-Amz-SignedHeaders=host&actor_id=0&response-content-disposition=attachment%3B%20filename%3Dgosu-amd64&response-content-type=application%2Foctet-stream' (ANSI_X3.4-1968) -> 'https://github-cloud.s3.amazonaws.com/releases/19708981/40d1b00c-8619-11e5-8953-d0122dcf07b9?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAISTNZFOVBIJMK3TQ/20160918/us-east-1/s3/aws4_request&X-Amz-Date=20160918T173223Z&X-Amz-Expires=300&X-Amz-Signature=3f340343a6f1b4d568a1d4ecb2af06c1e766e006ff5ea2c2d354d45c148d163b&X-Amz-SignedHeaders=host&actor_id=0&response-content-disposition=attachment; filename=gosu-amd64&response-content-type=application/octet-stream' (UTF-8)
--2016-09-18 17:32:24--  https://github-cloud.s3.amazonaws.com/releases/19708981/40d1b00c-8619-11e5-8953-d0122dcf07b9?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAISTNZFOVBIJMK3TQ/20160918/us-east-1/s3/aws4_request&X-Amz-Date=20160918T173223Z&X-Amz-Expires=300&X-Amz-Signature=3f340343a6f1b4d568a1d4ecb2af06c1e766e006ff5ea2c2d354d45c148d163b&X-Amz-SignedHeaders=host&actor_id=0&response-content-disposition=attachment;%20filename=gosu-amd64&response-content-type=application/octet-stream
Resolving github-cloud.s3.amazonaws.com (github-cloud.s3.amazonaws.com)... 54.231.18.1
Connecting to github-cloud.s3.amazonaws.com (github-cloud.s3.amazonaws.com)|54.231.18.1|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 2698808 (2.6M) [application/octet-stream]
Saving to: '/usr/local/bin/gosu'

     0K .......... .......... .......... .......... ..........  1% 74.7K 35s
    50K .......... .......... .......... .......... ..........  3%  111K 28s
   100K .......... .......... .......... .......... ..........  5%  115K 26s
   150K .......... .......... .......... .......... ..........  7%  121K 24s
   200K .......... .......... .......... .......... ..........  9%  116K 23s
   250K .......... .......... .......... .......... .......... 11%  118K 22s
   300K .......... .......... .......... .......... .......... 13%  116K 21s
   350K .......... .......... .......... .......... .......... 15%  110K 21s
   400K .......... .......... .......... .......... .......... 17%  126K 20s
   450K .......... .......... .......... .......... .......... 18%  116K 19s
   500K .......... .......... .......... .......... .......... 20%  119K 19s
   550K .......... .......... .......... .......... .......... 22%  112K 18s
   600K .......... .......... .......... .......... .......... 24%  118K 18s
   650K .......... .......... .......... .......... .......... 26%  119K 17s
   700K .......... .......... .......... .......... .......... 28%  114K 17s
   750K .......... .......... .......... .......... .......... 30%  117K 16s
   800K .......... .......... .......... .......... .......... 32%  178K 16s
   850K .......... .......... .......... .......... .......... 34%  118K 15s
   900K .......... .......... .......... .......... .......... 36%  116K 15s
   950K .......... .......... .......... .......... .......... 37%  119K 14s
                      [...]
                      [...]

Step 9 : ENV GHOST_CONTENT /var/lib/ghost
---> Running in 61156b2cb537
---> b4d0a9e54b19
Removing intermediate container 61156b2cb537
Step 10 : RUN mkdir -p "$GHOST_CONTENT" && chown -R user:user "$GHOST_CONTENT"
---> Running in 49683136928e
---> 681806385936
Removing intermediate container 49683136928e
Step 11 : VOLUME $GHOST_CONTENT
---> Running in d0b7478efbda
---> 176ce970d008
Removing intermediate container d0b7478efbda
Step 12 : COPY docker-entrypoint.sh /entrypoint.sh
---> df254620db94
Removing intermediate container fb8a57cf6f9b
Step 13 : ENTRYPOINT /entrypoint.sh
---> Running in ef5ac64665fc
---> e309f1dc79d2
Removing intermediate container ef5ac64665fc
Step 14 : EXPOSE 2368
---> Running in 49ce8d5c291d
---> d7e9bacd0ed2
Removing intermediate container 49ce8d5c291d
Step 15 : CMD npm start
---> Running in 9852f53a50b6
---> 370a54dfe27f
Removing intermediate container 9852f53a50b6
Successfully built 370a54dfe27f
                [...]
```  

Let us verify the image has been created or not  
```
docker images

```  

[Output]  

```
REPOSITORY            TAG                 IMAGE ID            CREATED             SIZE
mydockerhubid/ghost   0.2.0               370a54dfe27f        4 minutes ago       389.6 MB
node                  4-slim              48f7a334e4da        2 weeks ago         207.1 MB
```  

Validate the image is working by launching it  

```
docker run --name ghost2 -P  -itd mydockerhubid/ghost:0.2.0
```  

[Output]  

```
163118dad446505dc6539ad07e489e604c666f7158c72c4d19d76f00094b293a
```
Let us check the status of the container  
```
docker ps
```  

[Output]  

```
CONTAINER ID        IMAGE                       COMMAND                  CREATED              STATUS              PORTS                     NAMES
163118dad446        mydockerhubid/ghost:0.2.0   "/entrypoint.sh npm s"   About a minute ago   Up About a minute   0.0.0.0:32768->2368/tcp   ghost2
```  

```
docker port ghost2
```  

[Output]  

```
2368/tcp -> 0.0.0.0:32768
```

Let us verify the application by visiting, **http://HOST:PORT** which shows up ghost page.


### Dockerfile Primer  


| INSTRUCTION     | DESCRIPTION    |
| :------------- | :------------- |
| FROM       | The base image to use in the build. This is mandatory and must be the first command in the file      |
| MAINTAINER       | An optional value for the maintainer of the script      |
| RUN       | Executes a command and save the result as a new layer      |
| LABEL       | Adds metadata to an image      |
| ENV       | 	Sets an environment variable in the new container      |
| COPY       | Copies a file from the host system onto the container      |
| ADD       | 	Copies a file from the host system onto the container(Advanced than COPY)      |
| VOLUME       | Creates a shared volume that can be shared among containers or by the host machine      |
| USER       | Sets the user name or UID to use when running the image      |
| CMD       | 	The command that runs when the container starts      |
| ENTRYPOINT       | The command that runs when the container starts and takes runtime parameters      |
| ONBUILD       | 	A command that is triggered when the image in the Dcokerfile is used as a base for another image      |
| STOPSIGNAL       | Sets the system call signal that will be sent to the container to exit      |
| HEALTHCHECK       | Tells Docker how to test a container to check that it is still working      |
| SHELL       | Allows the default shell used for the shell form of commands to be overridden      |
| WORKDIR       | 	Set the default working directory for the container      |
| ARG | Defines a variable that users can pass at build-time to the builder with the docker build command using the --build-arg <varname>=<value> flag |


### Inefficient RUN Instructions  

As used in the reference Dockerfile, you have built the ghost image, its useful to combine multiple commands into a single RUN instruction. This is because each of the instructions are going to create a layer.

Lets see what happens if you have inefficient RUN instructions.

In the app directory that you downloaded earlier, examine Dockerfile.inef, and see if you could spot the difference between this and previous Dockerfile that you used.

Now, lets attempt building an image with Dockerfile.inef.

```
docker build -t mydockerhubid/ghost:inef -f Dockerfile.inef .
```

Now examine the difference between the images created with two different Dockerfiles

docker images | grep ghost  

### Tagging Images  
We can tag image with desired repository. This can be achieved by following the below syntax  

```
docker tag IMAGE HUB_USERNAME/REPO:TAG

```

e.g.

```
docker tag 20ebdc62d89b mydockerhubid/ghost:latest  

```  
Replace #mydockerhubid with your docker hub id  

Let us validate the tagged image is in the list of no

#### Exercise:  
Find out the id of 0.2.0 image you build with dockerfile and tag it as latest.  


### Pushing Images to Registry  
We can use DockerHub registry to save our images. These images can either be private or be public. First log in to DockerHub by running,   

```
docker login
```  

[Output]  

```
Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
Username: YOUR_DOCKERHUB_ID
Password: YOUR_DOCKERHUB_PASSWORD
Login Succeeded
```  

Let us push the ghost image that we have created using Dockerfile  

```
docker push mydockerhubid/ghost:0.2.0
docker push mydockerhubid/ghost:latest
```  

[Output]  

```
The push refers to a repository [docker.io/dialectpython/ghost]
1ebb83d1c095: Pushed
85db16821dc0: Pushed
dae3fd4d8f65: Pushed
183fa3b0a41b: Pushed
a5ae0cdecf97: Pushed
d8a2dd69eab2: Pushed
063d700495d9: Pushed
b5606c271900: Pushed
17587239b3df: Pushed
9e63c5bce458: Pushed
latest: digest: sha256:664be48340de2f3a201869ec7a5faa4c721b6758b0ab94063753a15b9efa16e1 size: 2413  

```  
Let us validate whether this image has been uploaded to our Dockerhub registry or not  

![hub](images/chp6/hub4.png)  

### Create Automated Builds  

After having published our images to Dockerhub, we are also going to setup a process to create automated builds.  

#### Step 1  

![hub](images/chp6/hub5.png)  

#### Step 2  

![hub](images/chp6/hub6.png)  

#### Step 3  

![hub](images/chp6/hub7.png)  

#### Step 4  

![hub](images/chp6/hub8.png)  

#### Step 5  

![hub](images/chp6/hub8.png)  

#### Step 6  

Authorize DockerHub application on Github  

#### Step 7  

Again go back to DockerHub dashboard and click on the following link  

![hub](images/chp6/hub5.png)  

#### Step 8  

![hub](images/chp6/hub9.png)  

#### Step 10  

![hub](images/chp6/hub10.png)  

#### Step 11  

![hub](images/chp6/hub11.png)  

#### Step 12  

![hub](images/chp6/hub12.png)  

There you go... You have created an automated build on DockerHub

   Docker Registry

The Registry is a stateless, highly scalable server side application that stores and lets you distribute Docker images.

## Setting up the Docker Registry

>docker run -d -p 5000:5000 --name registry registry:2

This pulls the registry:2 image from the docker hub and runs the docker container. The name of the container is Registry.

>docker pull ubuntu && docker tag ubuntu localhost:5000/myfirstimage

This pulls the ubuntu image from the docker hub. And we tag the image to localhost:5000/myfirstimage

>docker push localhost:5000/myfirstimage

When we try to push the image, it locally saves in the host file system. This we call as the __Docker Registry__

To stop the Registry we use

>docker stop registry

To remove Registry with all the data
>docker rm -v registry

## Docker Private Registry.

Docker Private Registry is to deploy the docker images present in one VM or host to another VM or Host.

Create a file system like given below in the host computer
```
.
├── Docker
│   └── Vagrantfile
└── Docker-Client
    └── Vagrantfile
```

Both vagrant file of the same Docker Box file.

Change the ip in the both the Vagrentfile as "192.168.33.10" and "192.168.33.11"

Now bring up the VM in the Docker directory.

We need to install Docker Compose first.

>yum install python-pip


pip install docker-compose


### Setting Docker Registry

After isntalling Docker Compose, its time to setup the .yml file for the Docker Compose.
Since we need a place to store the list of users who can access our Registry we need a place to store it. So we are going to install httpd-tools which contains the package called as __htpasswd__

>yum install httpd-tools


mkdir ~/docker-registry && cd $_


mkdir data

In the docker-registry, we create the .yml file for compose.


>vim docker-compose.yml

Now add the following contents contents
```
registry:
  image: registry:2
  ports:
    - 127.0.0.1:5000:5000
  environment:
    REGISTRY_STORAGE_FILESYSTEM_ROOTDIRECTORY: /data
  volumes:
    - ./data:/data
```


    Now save the file. And run docker compose.

>docker-compose up

### Setting Nginx container

    Edit docker compose file so that we can add the configurations for Nginx.
>vim docker-compose.yml

Add the contents
```
nginx:
  image: "nginx:1.9"
  ports:
    - 5043:443
  links:
    - registry:registry
  volumes:
    - ./nginx/:/etc/nginx/conf.d:ro
```

The full docker-compose.yml looks like

```
nginx:
  image: "nginx:1.9"
  ports:
    - 5043:443
  links:
    - registry:registry
  volumes:
    - ./nginx/:/etc/nginx/conf.d
registry:
  image: registry:2
  ports:
    - 127.0.0.1:5000:5000
  environment:
    REGISTRY_STORAGE_FILESYSTEM_ROOTDIRECTORY: /data
  volumes:
    - ./data:/data
  ```

Now we going to  edit the registry configuarations for the SSL certification

>vim ~/docker-registry/nginx/registry.conf

Add the following contents
```
  upstream docker-registry {
  server registry:5000;
}

server {
  listen 443;
  server_name myregistrydomain.com;

  # SSL
  # ssl on;
  # ssl_certificate /etc/nginx/conf.d/domain.crt;
  # ssl_certificate_key /etc/nginx/conf.d/domain.key;

  # disable any limits to avoid HTTP 413 for large image uploads
  client_max_body_size 0;

  # required to avoid HTTP 411: see Issue #1486 (https://github.com/docker/docker/issues/1486)
  chunked_transfer_encoding on;

  location /v2/ {
    # Do not allow connections from docker 1.5 and earlier
    # docker pre-1.6.0 did not properly set the user agent on ping, catch "Go *" user agents
    if ($http_user_agent ~ "^(docker\/1\.(3|4|5(?!\.[0-9]-dev))|Go ).*$" ) {
      return 404;
    }

    # To add basic authentication to v2 use auth_basic setting plus add_header
    # auth_basic "registry.localhost";
    # auth_basic_user_file /etc/nginx/conf.d/registry.password;
    # add_header 'Docker-Distribution-Api-Version' 'registry/2.0' always;

    proxy_pass                          http://docker-registry;
    proxy_set_header  Host              $http_host;   # required for docker client's sake
    proxy_set_header  X-Real-IP         $remote_addr; # pass on real client's IP
    proxy_set_header  X-Forwarded-For   $proxy_add_x_forwarded_for;
    proxy_set_header  X-Forwarded-Proto $scheme;
    proxy_read_timeout                  900;
  }
}
```

Save the file and exit

Now again start the docker compose.

>docker-compose up

To check whether Docker Rregistry is working or not try the following command

>curl http://localhost:5000/v2/

The output will be {}

And also try
>curl http://localhost:5043/v2/
The output will be {}

Next we going to create user and  their password who can login and access our Docker Registry
>cd ~/docker-registry/nginx

htpasswd -c registry.password USERNAME

For the first time when we run the command we use the option -c so that it creates the file. After that we dont need to use that option when we create Username

Now in the registry.conf which we created we are going to make some changes


>vim ~/docker-registry/nginx/registry.conf

Delete the below lines and
```
# To add basic authentication to v2 use auth_basic setting plus add_header
# auth_basic "registry.localhost";
# auth_basic_user_file /etc/nginx/conf.d/registry.password;
# add_header 'Docker-Distribution-Api-Version' 'registry/2.0' always;
```

And add the following lines
```
# To add basic authentication to v2 use auth_basic setting plus add_header
auth_basic "registry.localhost";
auth_basic_user_file /etc/nginx/conf.d/registry.password;
add_header 'Docker-Distribution-Api-Version' 'registry/2.0' always;
```

Now we are going to start the Docker Compose to see the changes  that we have done in the configuration file.
>cd ~/docker-registry

docker-compose up

Now check the in the command line
>curl http://localhost:5043/v2/

Output will be
```
<html>
<head><title>401 Authorization Required</title></head>
<body bgcolor="white">
<center><h1>401 Authorization Required</h1></center>
<hr><center>nginx/1.9.7</center>
</body>
</html>
```

This is because we we have given the registry.password file for the authentication.

Now try the below command to check
>curl http://USERNAME:PASSWORD@localhost:5043/v2/


### Setitng the ssl certificates

For SSL certificate go to the registry.conf files and do the following changes


>nano ~/docker-registry/nginx/registry.conf

Delete the following lines of code
```
server {
listen 443;
server_name myregistrydomain.com;
# SSL
# ssl on;
# ssl_certificate /etc/nginx/conf.d/domain.crt;
# ssl_certificate_key /etc/nginx/conf.d/domain.key;
```

And add these lines

```
# SSL
ssl on;
ssl_certificate /etc/nginx/conf.d/domain.crt;
ssl_certificate_key /etc/nginx/conf.d/domain.key;
```

Save and exit the file.

### Creating and Signing the Certificates

Now we are going to create and sign the SSL certificate.

>cd ~/docker-registry/nginx

 Generating the root key:
openssl genrsa -out devdockerCA.key 2048

Generating the root certificate(Press Enter whenever it prompts):
penssl req -x509 -new -nodes -key devdockerCA.key -days 10000 -out devdockerCA.crt

Generating the key for the server:
openssl genrsa -out domain.key 2048

Now we are going to send a certificate signing request.

Press Enter whenever it prompts and when it asks for the "_Common Name_" type the ip of the machine or the server address (Which you have given in registry.conf near server_name)

__Donate create a challenging password__
>openssl req -new -key domain.key -out dev-docker-registry.com.csr

Now we are going to sign the certificates request


>openssl x509 -req -in dev-docker-registry.com.csr -CA devdockerCA.crt -CAkey devdockerCA.key -CAcreateserial -out domain.crt -days 10000


Since the certificates are signed by ourself not by the Certificate Authority we have to tell the docker client that we have the authorized certificates. NOow we are going to do that locally
>update-ca-trust force-enable

cp domain.crt /etc/pki/ca-trust/source/anchors/

update-ca-trust extract

Restart the docker service and run the docker compose file.

>sudo service docker restart

cd ~/docker-registry

docker-compose up

To check the output:
>curl https://USERNAME:PASSWORD@[YOUR-DOMAIN]:5043/v2/

Changing the ports of the Nginx from 5043 to 443 in docker-compose.yml

Change it from
```
    - 5043:443
```
to
```
    - 443:443
```
Save and exit
Run the compose file

>docker-compose up

To check the output:
>curl https://<YOURUSERNAME>:<YOURPASSWORD>@YOUR-DOMAIN/v2/

###Accessing Your Docker Registry from a Client Machine

Now we have to copy the devdockerCA file from the Registry VM to the Client VM so that we can access the Docker Registry.


>sudo cat /docker-registry/nginx/devdockerCA.crt


Copy the above data in the file,

#####ON CLIENT MACHINE:

Paste the data present in the devdockerCA.crt in the below file
>vim /etc/pki/ca-trust/source/anchors/debdockerCA.crt

Now update the certificates and restart the docker service
>update-ca-trust extract

service docker restart

Now we can access the Docker Registry that is present in the Other VM by

>docker login https://YOUR-DOMAIN

Username: USERNAME

Password: PASSWORD


After entering the correct username and their passowrd we must get the following output
>"Login Succeeded"

Now lets just pull and run ubuntu images. Do some changes in it and try pusing it to the docker registry.


>docker run -t -i ubuntu /bin/bash

touch initcron

exit

docker commit $(docker ps -lq) test-image

Now lets login to the registry and push the changes that we made in the ubuntu container.
>docker login https://YOUR-DOMAIN

Username: USERNAME

Password: PASSWORD

docker tag test-image [YOUR-DOMAIN]/test-image

docker push [YOUR-DOMAIN]/test-image


Output will be like
```
latest: digest: sha256:5ea1cfb425544011a3198757f9c6b283fa209a928caabe56063f85f3402363b4 size: 8008
```

Now check it we can go back to the server and follow the steps
>docker pull [YOUR-DOMAIN]/test-images

docker run -t -i [YOUR-DOMAIN]/test-images /bin/bash

ls

Now here we can see that the file which we created "initcron" is available.
The Docker Private Registry is successfully configured.

 ### Docker Swarm Quick Dive
#### With Swarm Mode ( Docker version 1.12)

```

docker-machine create -d virtualbox master

docker-machine create -d virtualbox node1

docker-machine create -d virtualbox node2

```

##### In window 1

```
docker-machine env master

[execute the command to setup env ]

docker swarm init --advertise-addr <IP_ADDRESS_OF_MASTER>

docker node ls
```

##### In window 2

```
docker-machine env node1

docker swarm join \
    --token <TOKEN> \
    <IP_ADDRESS_OF_MASTER>
```

##### In window 3

```
docker-machine env node1

docker swarm join \
    --token <TOKEN> \
    <IP_ADDRESS_OF_MASTER>
```

### In window 1

```
docker node ls

docker service create --replicas 1 --name helloworld alpine ping docker.com

docker service ls

docker service inspect --pretty helloworld

docker service scale helloworld=5


docker service ps helloworld

docker node ps node1


docker service rm helloworld
```

  
  
