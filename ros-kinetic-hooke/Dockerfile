# Build:
#  podman build --rm --format docker -f Dockerfile -t re-je/ros-noetic-hooke .
#
# Usage:
#  docker pull ghcr.io/re-je/ros-noetic-hooke:main

FROM docker.io/gramaziokohler/ros-kinetic-moveit
LABEL maintainer "Gary Edwards <gary@re.je>"

SHELL ["/bin/bash","-c"]

ENV CATKIN_WS=/root/catkin_ws
ENV DEBIAN_FRONTEND=noninteractive

RUN echo "Building Kuka MoveIt Configs" \
    && source /opt/ros/${ROS_DISTRO}/setup.bash \
    && apt-get update && apt-get -y upgrade \
    # KUKA packages
    && git clone https://github.com/ros-industrial/kuka_experimental.git \
    && git clone https://github.com/re-je/kuka_kr150_2_moveit_config.git \
    # Install dependencies
    && cd $CATKIN_WS \
    && rosdep install -y --from-paths . --ignore-src --rosdistro ${ROS_DISTRO} \
    # Build catkin workspace
    && catkin_make \
    && rm -rf /var/lib/apt/lists/*
