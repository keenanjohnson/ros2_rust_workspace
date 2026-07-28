FROM ros:jazzy AS base
ARG DEBIAN_FRONTEND=noninteractive

##########################
## ros2_rust install
##########################
# Install Dependancies
RUN apt-get update && apt-get install -y \
    python3-vcstool \
    libclang-dev \
    curl \
    vim \
    clang \
    python3-pip \
    git \
    && rm -rf /var/lib/apt/lists/*

# Ubuntu 24.04 marks the system Python as externally managed (PEP 668),
# so pip needs --break-system-packages to install into it. No --upgrade:
# upgrading pytest would try to replace the Debian-owned pluggy package.
RUN pip install --break-system-packages pytest colcon-package-selection

# Install the colcon-cargo and colcon-ros-cargo plugins
RUN pip install --break-system-packages git+https://github.com/colcon/colcon-cargo.git git+https://github.com/colcon/colcon-ros-cargo.git

# Install Rust (same toolchain as upstream ros2_rust CI)
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- --default-toolchain 1.85.0 -y
ENV PATH=/root/.cargo/bin:$PATH

# Install the cargo-ament-build plugin
RUN cargo install --debug cargo-ament-build
