sudo apt-get install -y nvidia-container-toolkit on HOST machine first
(ref: https://github.com/nvidia/nvidia-docker/wiki/Installation-(Native-GPU-Support))

First build this image (docker build -t openrave-ha:v0, -->name this v0): https://github.com/jyf588/openrave-installation/blob/my_docker/nvidia-docker/Dockerfile (edited) 
Then build this image based on the previous one (name this v2): https://github.com/jyf588/openrave-installation/blob/my_docker/openrave-docker/Dockerfile (edited) 
Finally build this image based on the second one (name this v3): https://github.com/jyf588/openrave-installation/blob/my_docker/or-my-docker/Dockerfile (edited) 
Run container of the built image - use the commands: (create a container with access to data from the host machine create a folder "container_data" in the home directory)
xhost +si:localuser:root
sudo docker run --gpus=all -ti --rm -e DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix -v ~/container_data:/data --name openravecont openrave-ha:v3 /bin/bash
ALWAYS TYPE source bashrc WHEN YOU BEGIN A NEW CONTAINER
Inside the running container, see if you can use Firefox and openrave with GUI (refer to my Dockerfile comments as well) (edited) 
Other useful docker commands (with sudo): docker ps --all (list containers) / docker rm -f contrainer_number (kill and remove container) / docker image list / docker image rm image_number (edited) 
