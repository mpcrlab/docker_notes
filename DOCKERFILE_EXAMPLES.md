# Example Dockerfiles

To figure out what specific commands mean and which one you should be using, check [here](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/).

Docker has 3 different commands (RUN, CMD, and ENTRYPOINT) that all run things in different ways. It's confusing. Instead of learning the differences, just copy someone else's Dockerfile where they do the same thing you want.

## Training MNIST
```Dockerfile
FROM pytorch/pytorch:1.0-cuda10.0-cudnn7-runtime

RUN pip install tensorboardX==1.6.0
WORKDIR /var
ADD mnist.py /var

ENTRYPOINT ["python", "/var/mnist.py"]
```
* This script assumes there will be a file called `mnist.py` in the same folder as the Dockerfile during the build.
* The `ADD` command copies `mnist.py` from the host to the `/var` folder of the container.

## Deep Learning for NLP, and a Jupyter Notebook
```Dockerfile
FROM nvidia/cuda:10.1-cudnn7-devel

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update
RUN apt-get install -y python3-dev python3-pip git g++ wget make
#RUN pip3 install notebook

RUN pip3 install numpy scipy matplotlib ipython notebook pandas sympy nose scikit-learn
RUN pip3 install torch torchvision keras transformers torchtext spacy
RUN python3 -m spacy download en_core_web_lg

WORKDIR /external

# Add Tini. Tini operates as a process subreaper for jupyter. This prevents
# kernel crashes.
ENV TINI_VERSION v0.18.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini
RUN chmod +x /usr/bin/tini
ENTRYPOINT ["/usr/bin/tini", "--"]

EXPOSE 8888
CMD ["jupyter", "notebook", "--port=8888", "--no-browser", "--ip=0.0.0.0", "--allow-root", "--NotebookApp.token=''", "--NotebookApp.password=''"]
```

## YoloV3 Object Detection with PyTorch in a Jupyter Notebook
```Dockerfile
#start with a CUDA image so we can use GPUs
FROM nvidia/cuda:10.1-cudnn7-runtime

#update and install python, git, and opencv
RUN apt-get update && \
DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
python3-dev python3-pip python3-setuptools git g++ wget make libopencv-dev

#install jupyter
RUN pip3 install ipython jupyter sympy nose

#clone the YoloV3 git repository and install all the required dependencies.
RUN git clone https://github.com/eriklindernoren/PyTorch-YOLOv3 yolov3 \
    && cd yolov3 \
    && pip3 install -r requirements.txt

#Create a folder called /external. This is where the jupyter notebook will run.
WORKDIR /external

# Add Tini. Tini operates as a process subreaper for jupyter. This prevents
# kernel crashes.
ENV TINI_VERSION v0.6.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini
RUN chmod +x /usr/bin/tini
ENTRYPOINT ["/usr/bin/tini", "--"]

EXPOSE 8888
CMD ["jupyter", "notebook", "--port=8888", "--no-browser", "--ip=0.0.0.0", "--allow-root", "--NotebookApp.token=''", "--NotebookApp.password=''"]
```

