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

#### Image Commands

| Command | Description |
| --- | --- |
| `docker image ls` | View Images on Host |
| `docker pull [REPOSITORY:TAG OR ID]` | Pull Image from Docker Hub |
| `docker image rm [REPOSITORY:TAG OR ID]` | Delete Image from Host |

