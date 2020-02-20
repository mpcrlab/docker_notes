# What is Docker?

* Docker is virtual machine technology for the cloud.
* It runs a single service (webserver, database, neural network training job) in an isolated environment.
* Thousands of copies of a service can be run in parallel on a computing cluster, enabling webserver code to handle millions of requests or machine learning code to run faster in parallel.

### Why Use Docker?

* You will save a lot of time configuring computers and code.
* Other people have already used docker for you to do the things you want, and you can just steal their work.
* We can use Docker to scale parallel compute tasks like neural network training from a single desktop to a whole computing cluster, with minimal code changes.
* Docker sacrifices safety for performance, so your code will run just as fast as it would normally.

![https://www.researchgate.net/profile/Angel_Beltre/publication/333259856/figure/fig1/AS:761199041998851@1558495402272/Docker-Swarm-service-containers-spread-across-an-overlay-network.png](https://www.researchgate.net/profile/Angel_Beltre/publication/333259856/figure/fig1/AS:761199041998851@1558495402272/Docker-Swarm-service-containers-spread-across-an-overlay-network.png)

### Why NOT Use Docker?

* Some of the time you save configuring computers and code will be spent configuring docker.
* You have to get familiar with terminal commands and docker-specific instructions. (As of February 2020, I haven't found a good GUI or web interface that can control docker with GPU runtimes.)
* Each docker image will take up a few extra gigabytes of hard drive space on your computer.

### When should I use Docker?

* If you need to work on multiple computers and don't want to set up your development environment twice.
* If you need different versions of the same software (i.e. CUDA Toolkit versions) on the same computer.
* If you are having trouble running someone else's software and it is available in a docker container.
* If you need a reliable way to share your entire research/development environment so someone else can run your code.

### Some Definitions:

* Host Machine: The operating system running on your computer. Docker is installed and run on the host machine.
* Container: A virtual machine that runs in its own, isolated environment on your host machine. Each container has its own filesystem and network ports separate from the host, but shares basic operating system files so programs in the container still run fast.
* Image: A collection of big zip files stored on your host machine. They contain the operating system, libraries, and files you want to use in a container. Images are used to create and run containers.

![https://docs.docker.com/engine/images/engine-components-flow.png](https://docs.docker.com/engine/images/engine-components-flow.png)

* Dockerfile: A list of command-line-style instructions that tell Docker how to create an Image. Commands are used to say what operating system or base image to start with, what libraries/files to add, and finally what program to run when a container is created from the image.

![https://d3nmt5vlzunoa1.cloudfront.net/dotnet/files/2019/05/docker-cmds-complete.png](https://d3nmt5vlzunoa1.cloudfront.net/dotnet/files/2019/05/docker-cmds-complete.png)

* Docker Daemon: A service that runs in the background on your host computer and manages docker containers for you. It responds to requests from the Client.
* Docker Client: A program that you can call from the command line to send instructions to the Docker Daemon. You can use this to download/create/run/delete images and containers.
* Bind Mount: Docker containers have their own filesystem separate from your host's. To read files on your host INSIDE a container, you can "mount" a host folder to a folder in the container's filesystem.
* Bind Port: Containers also have their own network. Programs in a container like jupyter or tensorboard that run webservers on ports (i.e. localhost:8888) won't be visible outside the container. You can bind a port in the container to a port on your host network (i.e. bind localhost:8888 in the container to localhost:7777 on your host).

![https://docs.docker.com/engine/images/architecture.svg](https://docs.docker.com/engine/images/architecture.svg)


* Docker Hub Registry: DockerHub is like GitHub, but for Docker Images. The Docker Client automatically will pull/run images directly from the Hub if they don't already exist on your computer. You can create a Docker Hub account and upload your own images. Mine are located at [https://hub.docker.com/u/pmorris2012](https://hub.docker.com/u/pmorris2012).

![https://solutionsanz.files.wordpress.com/2017/08/github-dockerhub1.png?w=1200](https://solutionsanz.files.wordpress.com/2017/08/github-dockerhub1.png?w=1200)

* NVIDIA CUDA Driver: Like the docker daemon, this is a service that runs in the background and manages GPUs on your host computer. You need this installed to use GPUs at all, regardless of Docker.
* nvidia-docker: An add-on package to Docker that NVIDIA made so containers can use GPUs. This gets installed after Docker and the CUDA Driver.


# 
