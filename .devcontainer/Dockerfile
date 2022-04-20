# Ros2 Foxy runs on ubuntu focal
FROM ghcr.io/keenanjohnson/ros2_rust_workspace:main
ARG DEBIAN_FRONTEND=noninteractive

# Install the ros2 messages
RUN mkdir src
WORKDIR /src/
# Copy the .repos file into container for vcs
COPY . .
RUN vcs import /src < /src/ros2.repos

# Build the binaries
WORKDIR /src/src/
#RUN . /opt/ros/foxy/setup.sh && colcon build --packages-up-to rclrs_examples

# Set up auto-source of workspace for ros user
#ARG WORKSPACE
#RUN echo "if [ -f ${WORKSPACE}/install/setup.bash ]; then source ${WORKSPACE}/install/setup.bash; fi" >> ~/.bashrc
