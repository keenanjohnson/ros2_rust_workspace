# ROS 2 Jazzy runs on Ubuntu Noble.
# CI overrides BASE_IMAGE with an image built fresh from base_dockerfile/,
# so it never depends on a stale published image.
ARG BASE_IMAGE=ghcr.io/keenanjohnson/ros2_rust_workspace:main
FROM ${BASE_IMAGE}
ARG DEBIAN_FRONTEND=noninteractive

# Set up auto-source of workspace for ros user
ARG WORKSPACE
RUN echo "if [ -f ${WORKSPACE}/install/setup.bash ]; then source ${WORKSPACE}/install/setup.bash; fi" >> ~/.bashrc
