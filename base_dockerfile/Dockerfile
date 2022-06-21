FROM ros:foxy as base
ARG DEBIAN_FRONTEND=noninteractive

##########################
## Rust Install
##########################
# Install Dependancies
RUN apt-get update && apt-get install -y \
    curl \
    && rm -rf /var/lib/apt/lists/*

RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- --default-toolchain 1.61.0 -y
ENV PATH=/root/.cargo/bin:$PATH

##########################
## ros2_rust install
##########################
# Install Dependancies
RUN apt-get update && apt-get install -y \
    python3-vcstool \
    libclang-dev \
    clang \
    python3.9 \
    python3.9-dev \
    python3-pip \
    git \
    && rm -rf /var/lib/apt/lists/*

RUN pip install --upgrade pytest colcon-package-selection

# Install the colcon-cargo and colcon-ros-cargo plugins
RUN pip install git+https://github.com/colcon/colcon-cargo.git git+https://github.com/colcon/colcon-ros-cargo.git

# Install the cargo-ament-build plugin 
RUN cargo install --debug cargo-ament-build

# Import ROS Deps
WORKDIR /workspaces/ros2_rust_workspace/
COPY ros2.repos .
RUN vcs import /workspaces/ros2_rust_workspace/src < /workspaces/ros2_rust_workspace/src/ros2.repos

# Build Rust / ROS2 Examples
RUN source /opt/ros/foxy/setup.bash && colcon build --packages-up-to examples_rclrs_message_demo

