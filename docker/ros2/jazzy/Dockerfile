# https://github.com/osrf/docker_images/blob/master/README.md#ros---1
# https://github.com/osrf/docker_images/blob/master/ros/jazzy/ubuntu/noble/desktop/Dockerfile

# This is an auto generated Dockerfile for ros:desktop
# generated from docker_images_ros2/create_ros_image.Dockerfile.em
ARG ROS_DISTRO=jazzy
FROM ros:${ROS_DISTRO}-ros-base-noble

ARG ros_ws=/home/ubuntu/dev_ws

ENV DEBIAN_FRONTEND=noninteractive

# Install packages.
RUN apt-get update && apt-get install -y --no-install-recommends \
    ros-${ROS_DISTRO}-desktop \
    ros-${ROS_DISTRO}-gazebo-* \
    ros-${ROS_DISTRO}-joint-state-publisher-gui \
    ros-${ROS_DISTRO}-ros2-control \
    ros-${ROS_DISTRO}-ros2-control-test-assets \
    ros-${ROS_DISTRO}-ros2-controllers \
    ros-${ROS_DISTRO}-hardware-interface-testing \
    ros-${ROS_DISTRO}-xacro \
    ros-${ROS_DISTRO}-joint-state-publisher-gui \
    python-is-python3 \
    pre-commit \
    vim \
    less \
    joystick \
    xterm

RUN adduser ubuntu sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

# Switch to a non-root user.
USER ubuntu

# Working directory
WORKDIR /home/ubuntu

# ENVs
ENV HOME=/home/ubuntu
ENV PATH="/home/ubuntu/.local/bin:${PATH}"

# Force Python stdout and stderr streams to be unbuffered.
ENV PYTHONUNBUFFERED 1

# Add sourcing to your shell startup script
# https://docs.ros.org/en/galactic/Tutorials/Configuring-ROS2-Environment.html#add-sourcing-to-your-shell-startup-script
RUN echo "source /opt/ros/${ROS_DISTRO}/setup.bash" >> ~/.bashrc

# Add `colcon_cd` to your shell startup script
# https://docs.ros.org/en/galactic/Tutorials/Configuring-ROS2-Environment.html#add-colcon-cd-to-your-shell-startup-script
RUN echo "source /usr/share/colcon_cd/function/colcon_cd.sh" >> ~/.bashrc \
    && echo "export _colcon_cd_root=${ros_ws}" >> ~/.bashrc

# https://github.com/ros2/ros2/issues/1531
RUN echo "ulimit -n 1024" >> ~/.bashrc

# This entrypoint is from base image.
# See https://github.com/osrf/docker_images/blob/master/ros/galactic/ubuntu/focal/ros-core/ros_entrypoint.sh
ENTRYPOINT ["/ros_entrypoint.sh"]

CMD ["sleep", "infinity"]
