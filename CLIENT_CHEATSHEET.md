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
| `docker build .` | Build Image from the Dockerfile in the current folder. |
| `docker build -f Dockerfile .` | Build Image with a specific Dockerfile |
| `docker build -f Dockerfile -t [NAME:TAG] .` | Build Image with name and tag |

#### Manage Containers

| Command | Description |
| --- | --- |
| `docker container ls` | List Running Containers |
| `docker container ls -a` | List All Containers |
| `docker start [CONTAINER]` | Start a Stopped Container |
| `docker stop [CONTAINER]` | Stop a Running Container |
| `docker container rm [CONTAINER]` | Delete a Stopped Container |
| `docker rename [CONTAINER] [NEW_NAME]` | Rename container |

