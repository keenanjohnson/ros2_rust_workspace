FROM althack/ros2:foxy-dev 

# ** [Optional] Uncomment this section to install additional packages. **
#
# ENV DEBIAN_FRONTEND=noninteractive
# RUN apt-get update \
#    && apt-get -y install --no-install-recommends <your-package-list-here> \
#    #
#    # Clean up
#    && apt-get autoremove -y \
#    && apt-get clean -y \
#    && rm -rf /var/lib/apt/lists/*
# ENV DEBIAN_FRONTEND=dialog

##########################
## Rust Install
##########################
# Install Dependancies
RUN apt-get update && apt-get install -y \
    curl \
    && rm -rf /var/lib/apt/lists/*

RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- --default-toolchain 1.59.0 -y
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
RUN cargo install cargo-ament-build

# Install the ros2 messages
# Copy the .repos file into container for vcs
COPY . .
RUN vcs import --skip-existing < src/ros2.repos src

RUN . /opt/ros/foxy/setup.sh && colcon build --packages-up-to rclrs_examples

# Set up auto-source of workspace for ros user
#ARG WORKSPACE
#RUN echo "if [ -f ${WORKSPACE}/install/setup.bash ]; then source ${WORKSPACE}/install/setup.bash; fi" >> ~/.bashrc
