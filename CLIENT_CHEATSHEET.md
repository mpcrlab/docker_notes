# Docker Client Cheatsheet

#### Refer to Images in Commands

| Format | Example |
| --- | --- |
| `[REPOSITORY]` | `ubuntu` |
| `[REPOSITORY:TAG]` | `ubuntu:latest` |
| `[IMAGE ID]` | `a2a15febcdf3` |

#### Refer to Containers in Commands

| Format | Example |
| --- | --- |
| `[NAME]` | `bold_beaver` |
| `[CONTAINER ID]` | `51a372c56e8a` |

#### Manage Images

| Command | Description |
| --- | --- |
| `docker image ls` | View Images on Host |
| `docker pull [IMAGE]` | Pull Image from Docker Hub |
| `docker image rm [IMAGE]` | Delete Image from Host |

### Build Images

| Command | Description |
| --- | --- |
| `docker build .` | Build Image from Dockerfile in current folder |
| `docker build -f Dockerfile .` | Build Image with a specific Dockerfile |
| `docker build -t [NAME:TAG] .` | Build Image with [NAME] and [TAG] |

#### Manage Containers

| Command | Description |
| --- | --- |
| `docker container ls` | List Running Containers |
| `docker container ls -a` | List All Containers |
| `docker start [CONTAINER]` | Start a Stopped Container |
| `docker stop [CONTAINER]` | Stop a Running Container |
| `docker container rm [CONTAINER]` | Delete a Stopped Container |
| `docker rename [CONTAINER] [NEW_NAME]` | Rename container |

#### Run Containers

| Command | Description |
| --- | --- |
| `docker run [IMAGE]` | Run container with default CMD |
| `docker run -it [IMAGE] /bin/bash` | Start with an Interactive Terminal |
| `docker exec -it [CONTAINER] /bin/bash` | Open Interactive Terminal in Running Container |
| `docker run [IMAGE] [YOUR_PROGRAM]` | Start container with [YOUR_PROGRAM] command |
| `docker exec [CONTAINER] [YOUR_PROGRAM]` | Run [YOUR_PROGRAM] in Running Container |
| `docker run --rm [IMAGE]` | Run container in auto-remove mode |
| `docker run -p [HOST_PORT]:[CONTAINER_PORT] [IMAGE]` | Start Container with Port Forward |
| `docker run -v [HOST_FOLDER]:[CONTAINER_FOLDER] [IMAGE]` | Start Container with Volume Mount |
| `docker run --gpus all [IMAGE]` | Use Nvidia-Docker Runtime |
| `docker run --gpus 2 [IMAGE]` | Specify # of GPUs |
| `docker run --gpus '"device=0,1"' [IMAGE]` | Specify GPU Device IDs |
| `docker run --ipc="host" [IMAGE]` | Use Host's Shared Memory to avoid multiprocessing errors |
| `docker run --name [NAME] [IMAGE]` | Start Container with name [NAME] |


