# Ros2 Foxy runs on ubuntu focal
FROM ghcr.io/keenanjohnson/ros2_rust_workspace:main
ARG DEBIAN_FRONTEND=noninteractive

# Set up auto-source of workspace for ros user
ARG WORKSPACE
RUN echo "if [ -f ${WORKSPACE}/install/setup.bash ]; then source ${WORKSPACE}/install/setup.bash; fi" >> ~/.bashrc
