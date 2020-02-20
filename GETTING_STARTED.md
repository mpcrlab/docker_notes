# Getting Started with the Docker Client

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
##### Open a terminal in a running container
```Shell Session
mpcrpaul@mpcrpaul-MS-7B61:~$ docker container ls
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
1289374395d5        ubuntu              "/bin/bash"         4 minutes ago       Up 15 seconds                           youthful_wiles
```
```Bash
docker exec -it youthful_wiles /bin/bash
```
* The `exec` command runs the `/bin/bash` program in our `youthful_wiles` container.
* The `-it` flags make the terminal interactive.
* You can open multiple terminals at the same time by running `exec` twice.
* `exec` can run any program in the container's filesystem, not just terminals.

---
##### Delete images and stopped containers
```Bash
docker rm ubuntu_terminal2
docker container rm ubuntu_terminal2
docker image rm ubuntu
```
* `rm` will remove either images or containers by their names/IDs.
* `container rm` and `image rm` are more verbose ways of saying the same thing.

---
##### Auto-delete a container after it finishes running
```Bash
docker run -it --rm ubuntu:latest /bin/bash
```
* The `--rm` flag will automatically delete the container after the terminal session ends.

---
##### Bind Port Forwards
```Bash
docker run -p 7777:8888 -p 7778:8889 jupyter/tensorflow-notebook
```
* The `-p` flag will add a port forward from the container to the host. Ports are given as [HOST]:[CONTAINER].
* In this case, a jupyter notebook is running at `localhost:8888` in the container by default.
* Since we mounted the container's port 8888 at our host's 7777, we will see the notebook at `localhost:7777` in the browser.
* Multiple `-p` flags can be given to forward multiple ports.

---
##### Bind Mount Volumes
```Bash
docker run -p 7777:8888 -v /home:/external jupyter/tensorflow-notebook
```
```Shell Session
jovyan@18066f01c6be:~$ ls /external
mpcrpaul  pmorris2012
```
* The `-v` flag will mount a host folder in the container's filesystem. Folder paths are given as [HOST]:[CONTAINER].
* In this case, our home folder will be located at `/external` in the container.
* Multiple `-v` flags can be given to mount multiple folders.

---
##### Run a container with GPUs
```Bash
docker run --gpus all -it nvidia/cuda:10.1-cudnn7-devel /bin/bash
docker run --gpus 1 -it nvidia/cuda:10.1-cudnn7-devel /bin/bash
docker run '"device=0,1"' -it nvidia/cuda:10.1-cudnn7-devel /bin/bash
```
* The `--gpus` flag will start a container with the Nvidia-Docker runtime.
* `all` will use all GPUs on the host. `1`, `2`, etc. will use 1 or 2 GPUs. Specific Device IDs can also be given.

---
##### Increase Shared Memory in a container
```Bash
docker run --gpus all -it --ipc="host" nvidia/cuda:latest /bin/bash
```
* If your code uses message passing (MPI) or other multiprocessing, it might need to share memory between processes.
* The `--ipc` flag sets the "inter-process communication" mode. Set it to `"host"` to allow all memory to be shared.
* If you get a weird error about a PyTorch dataloader process terminating early, this flag might fix it.

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
