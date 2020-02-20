# docker_notes
Notes on using docker for a development environment.

Disclaimer: These notes are tailored towards using docker to manage and share development environments for data science and machine learning in FAU's MPCR Lab.

# What is Docker?

* Docker is virtual machine technology for the cloud.
* It runs a single service (webserver, database, neural network training job) in an isolated environment.
* Thousands of copies of a service can be run in parallel on a computing cluster, enabling webserver code to handle millions of requests or machine learning code to run faster in parallel.

### Why Use Docker?

* You will save a lot of time configuring computers and code.
* Other people have already used docker for you to do the things you want, and you can just steal their work.
* We can use Docker to scale parallel compute tasks like neural network training from a single desktop to a whole computing cluster, with minimal code changes.
* Docker sacrifices safety for performance, so your code will run just as fast as it would normally.

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

* Docker Daemon:
* Docker Client:
* Docker Hub Registry:
* Bind Mount:

![https://docs.docker.com/engine/images/architecture.svg](https://docs.docker.com/engine/images/architecture.svg)

* NVIDIA CUDA Driver:
* nvidia-docker:
* Bind Port


# 
