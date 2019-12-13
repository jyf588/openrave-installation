FROM openrave-ha:v0

WORKDIR /root

# install ros (ros visualization and its packages can be useful when using OpenRave)
RUN sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'

RUN apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654 \
        && apt-get update \
        && apt-get install -y --no-install-recommends \
            ros-kinetic-desktop \
            ros-kinetic-catkin \
            libtinyxml2-dev \
            ros-kinetic-srdfdom \
            ros-kinetic-urdf-tutorial

# will be warning of running with root here, does not matter
RUN rosdep init && rosdep update

# https://github.com/docker/for-linux/issues/395
RUN echo "source /opt/ros/kinetic/setup.bash" >> /root/bashrc
WORKDIR /root

# RUN /bin/bash -c 'source /opt/ros/kinetic/setup.bash && echo $ROS_PACKAGE_PATH' 

# set up catkin workspace
RUN mkdir -p catkin_ws/src
WORKDIR /root/catkin_ws

RUN ["/bin/bash", "-c", "source /root/bashrc \
                         && echo $ROS_PACKAGE_PATH \
                         && catkin_make"]
RUN echo "source /root/catkin_ws/devel/setup.bash" >> /root/bashrc
WORKDIR /root

# install OMPL package

# temporary
WORKDIR /root/openrave-installation
RUN git pull

RUN ["/bin/bash", "-c", "source /root/bashrc \
                         && chmod u+x install-ompl-ubuntu.sh \
                         && ./install-ompl-ubuntu.sh --python"]
RUN apt-get install -y --no-install-recommends ros-kinetic-ompl
# the above is bit odd, as the ros binary of ompl does not contain python binding,
# but only installing from source is not enough because the path is not set properly

# set up openrave variables
ENV OPENRAVE_PLUGINS="/root/catkin_ws/devel/share/openrave-0.9/plugins:${OPENRAVE_PLUGINS}"
ENV LD_LIBRARY_PATH="$(openrave-config --python-dir)/openravepy/_openravepy_:${LD_LIBRARY_PATH}"
ENV PYTHONPATH="$(openrave-config --python-dir):${PYTHONPATH}"
ENV OPENRAVE_DATA="/root/git/openrave/src/data:${OPENRAVE_DATA}"

# install OMPL and URDF-parser for OpenRave
WORKDIR /root/catkin_ws/src
RUN git clone https://github.com/jyf588/or_urdf.git
# default branch is kinetic-fixes

# WORKDIR /root/catkin_ws/src/or_urdf
# RUN git checkout kinetic-fixes git checkout -b branchxyz origin/branchxyz
# WORKDIR /root/catkin_ws/src
RUN git clone https://github.com/personalrobotics/openrave_catkin.git
RUN git clone https://github.com/personalrobotics/or_ompl.git
WORKDIR /root/catkin_ws
RUN ["/bin/bash", "-c", "source /root/bashrc \
                         && catkin_make"]

WORKDIR /root

# "source /root/bashrc" when you run the container








