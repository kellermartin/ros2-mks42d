FROM ros:jazzy-ros-base

# Add vscode user with same UID and GID as your host system
# (copied from https://code.visualstudio.com/remote/advancedcontainers/add-nonroot-user#_creating-a-nonroot-user)
ARG USERNAME=ubuntu
RUN apt-get update \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME
# Switch from root to user
USER $USERNAME

# Add user to video group to allow access to webcam
RUN sudo usermod --append --groups video $USERNAME

# Update all packages
RUN sudo apt update && sudo apt upgrade -y

# Install Git
RUN sudo apt install -y git

# Install CAN
RUN sudo apt install -y can-utils net-tools iproute2 

# Install Ros 2 Control and Controllers
RUN sudo apt install -y ros-jazzy-ros2-control ros-jazzy-ros2-controllers
# Install additional dependencies for CANopen
RUN sudo apt install -y ros-jazzy-canopen ros-jazzy-canopen-ros2-control ros-jazzy-canopen-402-driver

# Rosdep update
RUN rosdep update

# Source the ROS setup file
RUN echo "source /opt/ros/${ROS_DISTRO}/setup.bash" >> ~/.bashrc

CMD ["/bin/bash"]
