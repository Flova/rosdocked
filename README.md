## rosdocked

🐳 ❤️ 🤖

Run ROS Melodic / Ubuntu Bionic within Docker on any platform with a shared username,
home directory, and X11. For ROS Kinetic, switch to the respective branch.

This enables you to build and run a persistent ROS Melodic workspace as long as
you can run Docker images.

Note that any changes made outside of your home directory from within the Docker environment will not persist. If you want to add additional binary packages or remove some of the dependencies that are currently installed, change the Dockerfile accordingly and rebuild.

For more info on Docker see here: https://docs.docker.com/engine/installation/linux/ubuntulinux/

### Install Docker

Install Docker on your system, add your user to the `docker` group (`sudo usermod -aG docker $USER`), log out and in again and start and enable the docker service (`sudo systemctl start docker && sudo systemctl enable docker`).

### Build

This will create the image with your user/group ID and home directory.

```
./build
```

### Run

This will run the docker image.

```
./run
```

The image shares it's network interface with the host, so you can run this in
multiple terminals for multiple hooks into the docker environment.

Additionally, a video device is shared with the container. This video device can be set in the `run` script and will appear in the container as `/dev/video0`.

The Docker image will use your own shell configuration. To provide different settings inside and outside of the container, you can make use of the `$DOCKER` environment variable that is set to `1` inside of the docker image. To make use of this put something like

```
if [[ -n "$DOCKER" ]]; then
    # Settings for inside of the docker
    export PROMPT="DOCKER $PROMPT"  # Prefix the prompt with DOCKER
    # source workspace, etc.
else
    # Settings for outside of the docker
fi
```

in your `.bashrc` or `.zshrc`.
