# references:
# https://gitlab.com/nvidia/container-images/samples/blob/master/opengl/ubuntu16.04/glxgears/Dockerfile
# https://github.com/nvidia/nvidia-docker/wiki/Installation-(Native-GPU-Support)

# running instructions:
# docker build -t openrave-ha:v0 .
# xhost +si:localuser:root
# docker run --gpus=all -ti --rm -e DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix openrave-ha:v0 /bin/bash
# inside contrainer, try running glxgears and firefox

# FROM nvidia/opengl:1.0-glvnd-runtime-ubuntu16.04
FROM nvidia/cudagl:10.0-devel-ubuntu16.04

ENV NVIDIA_DRIVER_CAPABILITIES ${NVIDIA_DRIVER_CAPABILITIES},display

RUN apt-get update && apt-get install -y --no-install-recommends \
        build-essential \
        mesa-utils \
        git \
        g++ \
        cmake \
        lsb-core \
        wget \
        mlocate \
	    vim \
	    firefox \
        && rm -rf /var/lib/apt/lists/*

WORKDIR /root
RUN git clone https://github.com/jyf588/openrave-installation.git
WORKDIR /root/openrave-installation
RUN mkdir -p /root/git
RUN ./install-dependencies.sh
RUN ./install-osg.sh
RUN ./install-fcl.sh
RUN ./install-openrave.sh
WORKDIR /root



