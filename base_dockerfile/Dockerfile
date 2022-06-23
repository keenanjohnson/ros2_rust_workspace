FROM ros:foxy as base
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
    curl \
    vim \
    python3.9 \
    python3.9-dev \
    python3-pip \
    git \
    && rm -rf /var/lib/apt/lists/*

RUN pip install --upgrade pytest colcon-package-selection

# Install the colcon-cargo and colcon-ros-cargo plugins
RUN pip install git+https://github.com/colcon/colcon-cargo.git git+https://github.com/colcon/colcon-ros-cargo.git

# Install Rust
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- --default-toolchain 1.61.0 -y
ENV PATH=/root/.cargo/bin:$PATH

# Switch Rust to the nightly build.
# Note we are currently using the nightly build for the 
# sparse update feature in crates.io index.
# Rustup switches to the nightly build
# See this blog post for more info on the spare-registry feature
# https://blog.rust-lang.org/2022/06/22/sparse-registry-testing.html
RUN rustup toolchain install nightly

# Install the cargo-ament-build plugin
RUN cargo +nightly install -Z sparse-registry --debug cargo-ament-build 
