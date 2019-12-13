FROM openrave-ha:v2

WORKDIR /root

WORKDIR /root/catkin_ws/src
RUN git clone https://github.com/jyf588/inmoov_ros.git
WORKDIR /root/catkin_ws/src/inmoov_ros
RUN rm sr_description
WORKDIR /root/catkin_ws/src
RUN git clone https://github.com/jyf588/shadow_hand_arm.git
WORKDIR /root/catkin_ws
RUN ["/bin/bash", "-c", "source /root/bashrc \
                         && catkin_make"]

WORKDIR /root
RUN wget https://packages.microsoft.com/repos/vscode/pool/main/c/code/code_1.41.0-1576089540_amd64.deb
RUN apt install -y ./code_1.41.0-1576089540_amd64.deb
# RUN curl https://packages.microsoft.com/keys/microsoft.asc \
#     | gpg --dearmor > packages.microsoft.gpg
# RUN install -o root -g root -m 644 packages.microsoft.gpg /usr/share/keyrings/
# RUN sh -c 'echo "deb [arch=amd64 signed-by=/usr/share/keyrings/packages.microsoft.gpg] \
#             https://packages.microsoft.com/repos/vscode \
#             stable main" > /etc/apt/sources.list.d/vscode.list'
# RUN apt-get install -y --no-install-recommends apt-transport-https
# RUN apt-get update
# RUN apt-get install -y --no-install-recommends code

# # download or planning scripts
# WORKDIR /root/git
# RUN git clone https://github.com/jyf588/or_planning_scripts.git















