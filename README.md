# Ros2 Rust Workspace

A template for developing ROS2 applications in Rust using VSCode as IDE inside of a Docker container

It uses the un-official (for now) [ros2_rust](https://github.com/ros2-rust/ros2_rust) project

## Status
This is still in development and might not yet work perfectly! Jump in and file issues or submit changes!

## Inspiration

I was heavily inspired by Allison Thackston's (@athackst)
[vscode_ros2_workspace](https://github.com/athackst/vscode_ros2_workspace),
so please check out that project and give it a star!

## How to use

You should already have Docker and VSCode with the remote containers plugin installed on your system.

* [docker](https://docs.docker.com/engine/install/)
* [vscode](https://code.visualstudio.com/)
* [vscode remote containers plugin](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

### Get the template

Click on "use this template" in the top right corner of this repo on the Github site.

### Create your repository

On the next dialog, name the repository you would like to start and decide if you want all of the branches, or just the main.

Github will then create a new repository with the contents of this one in your account.  It grabs the latest changes as "initial commit".

### Clone your repo

Now you can clone your repo as normal

### Open it in vscode

Now that you've cloned your repo onto your computer, you can open it in VSCode (File->Open Folder). 

When you open it for the first time, you should see a little popup that asks you if you would like to open it in a container.  Say yes!

If you don't see the pop-up, click on the little green square in the bottom left corner, which should bring up the container dialog

In the dialog, select "Remote Containers: Reopen in container"

VSCode will build the dockerfile inside of `.devcontainer` for you.  If you open a terminal inside VSCode (Terminal->New Terminal), you should see that your username has been changed to `ros`, and the bottom left green corner should say "Dev Container"

### Building the ROS Nodes
Once inside the container, it's easy to setup ROS and build the rust / ROS examples.

Setup ROS:
```
cd /workspaces/ros2_rust_workspace/
vcs import src < src/ros2_rust/ros2_rust_foxy.repos
. /opt/ros/foxy/setup.sh
colcon build --packages-up-to examples_rclrs_message_demo
```

This will build the examples from the ros2_rust project.

### Running the publisher and subscriber

Publisher:

```
# Do this in a new terminal
. ./install/setup.sh
ros2 run examples_rclrs_minimal_pub_sub minimal_publisher
```

Subscriber:

```
# Do this in a new terminal
. ./install/setup.sh
ros2 run examples_rclrs_minimal_pub_sub minimal_subscriber
```
