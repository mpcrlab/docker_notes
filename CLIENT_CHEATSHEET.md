# Docker Client Cheatsheet

##### View docker images currently downloaded on your host computer
```Bash
docker image ls
```
```Shell Script
mpcrpaul@mpcrpaul-MS-7B61:~$ docker image ls
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu              18.04               775349758637        3 months ago        64.2MB
ubuntu              latest              a2a15febcdf3        6 months ago        64.2MB
```
* Images can be referred to by their name (`ubuntu`), name and tag (`ubuntu:18.04`), or Image ID (`775349758637`).

---
##### Pull an image from Docker Hub
```Bash
docker pull nvidia/cuda:10.2-cudnn7-devel
```

---
##### Start a container from an image with an interactive terminal
```Bash
docker run -it ubuntu:latest /bin/bash
```
* The `-i` flag keeps an input pipe open so you can type commands into the container.
* The `-t` flag creates a terminal emulator.
* These can be combined into `-it`, which you can pretend stands for "interactive terminal" mode.
* The container is created from the latest `ubuntu` image. It will be downloaded from Docker Hub if it's not already on the host.
* The container will run the program located at `/bin/bash` in its filesystem, which is a bash terminal.

---
##### View running containers
```Bash
docker container ls
```
```Shell Session
mpcrpaul@mpcrpaul-MS-7B61:~$ docker container ls
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```
* If there are any containers running on your host, they will show up here.

---
##### View *all* containers, running or stopped
```Bash
docker container ls -a
```
```Shell Session
mpcrpaul@mpcrpaul-MS-7B61:~$ docker container ls -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS               NAMES
1289374395d5        ubuntu              "/bin/bash"         39 seconds ago      Exited (0) 37 seconds ago                       youthful_wiles
```
* The `-a` or `--all` flags show all containers
* Like images, containers can be referred to by their unique IDs (`1289374395d5`).
* Containers can also be referenced by the names they are randomly assigned at creation (`youthful_wiles`).

---
##### Start/Stop containers
```Bash
docker start youthful_wiles
```
```Shell Session
mpcrpaul@mpcrpaul-MS-7B61:~$ docker container ls
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
1289374395d5        ubuntu              "/bin/bash"         4 minutes ago       Up 15 seconds                           youthful_wiles
```
* The `start` command will start a stopped container, given its name or ID.
```Bash
docker stop youthful_wiles
```
```Shell Session
mpcrpaul@mpcrpaul-MS-7B61:~$ docker container ls
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```
* The `stop` command will stop a running container, given its name or ID.

---
##### Name/Rename containers
```Bash
docker run -it --name ubuntu_terminal ubuntu:latest /bin/bash
```
```Shell Session
mpcrpaul@mpcrpaul-MS-7B61:~$ docker container ls -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS               NAMES
686bee6107b5        ubuntu:latest       "/bin/bash"         30 seconds ago      Exited (0) 23 seconds ago                       ubuntu_terminal
```
* When running a container, the `--name [NAME]` flag will assign the container [NAME].
```Bash
docker rename ubuntu_terminal ubuntu_terminal2
```
```Shell Session
mpcrpaul@mpcrpaul-MS-7B61:~$ docker container ls -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                     PORTS               NAMES
686bee6107b5        ubuntu:latest       "/bin/bash"         2 minutes ago       Exited (0) 2 minutes ago                       ubuntu_terminal2
```
* The `rename` command will rename an existing container.
