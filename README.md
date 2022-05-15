```bash
###############################################################################################################################
##                                                                                                                           ##
##  ███    ███ ██ ███    ██ ███████  ██████ ██████   █████  ███████ ████████                  M A S T E R   O V E R V I E W  ##
##  ████  ████ ██ ████   ██ ██      ██      ██   ██ ██   ██ ██         ██                                                    ##
##  ██ ████ ██ ██ ██ ██  ██ █████   ██      ██████  ███████ █████      ██                                   B U I L D I N G  ##
##  ██  ██  ██ ██ ██  ██ ██ ██      ██      ██   ██ ██   ██ ██         ██                                                    ##
##  ██      ██ ██ ██   ████ ███████  ██████ ██   ██ ██   ██ ██         ██                                         U S A G E  ##
##                                                                                                                           ##
##  ████████ ██       █████  ██    ██ ███    ██  ██████ ██   ██ ███████ ██████                                               ##
##     ██    ██      ██   ██ ██    ██ ████   ██ ██      ██   ██ ██      ██   ██                                              ##
##     ██    ██      ███████ ██    ██ ██ ██  ██ ██      ███████ █████   ██████                                               ##
##     ██    ██      ██   ██ ██    ██ ██  ██ ██ ██      ██   ██ ██      ██   ██                                              ##
##     ██    ███████ ██   ██  ██████  ██   ████  ██████ ██   ██ ███████ ██   ██                                              ##
##                                                                                                                           ##
##   ██████ ██      ██ ███████ ███    ██ ████████       ██ ███    ██       ██████   ██████   ██████ ██   ██ ███████ ██████   ##
##  ██      ██      ██ ██      ████   ██    ██          ██ ████   ██       ██   ██ ██    ██ ██      ██  ██  ██      ██   ██  ##
##  ██      ██      ██ █████   ██ ██  ██    ██    █████ ██ ██ ██  ██ █████ ██   ██ ██    ██ ██      █████   █████   ██████   ##
##  ██      ██      ██ ██      ██  ██ ██    ██          ██ ██  ██ ██       ██   ██ ██    ██ ██      ██  ██  ██      ██   ██  ##
##   ██████ ███████ ██ ███████ ██   ████    ██          ██ ██   ████       ██████   ██████   ██████ ██   ██ ███████ ██   ██  ##
##                                                                                                                           ##
###############################################################################################################################
```

This project offers a quick way to spin up the **TLauncher Minecraft Client** within a Docker container.  There are numerous use cases for this, and if you've landed on this project, chances are you already have good reason.  This project uses the **OFFICIAL** TLauncher jar and not a self-hosted alternative.  I'll do my best to keep this reference up to date, but drop an issue down if you're finding it broken.

This repository is derived from [dm9pZCAq's](https://github.com/dm9pZCAq/docker-tlauncher) Dockerfile.

&nbsp;

### Environment Prerequisites:

Prior to running this image, you'll need to ***permit*** Docker on the local machine to connect to the X window display.  Run this command to do so:

```shell
xhost +local:docker
```

&nbsp;

### Build the image from GitHub

You can build this image directly from GitHub.  This scenario can be utilized when no changes to the image are required.

```shell
docker build -t tlauncher github.com/lukeawyatt/docker-tlauncher
```

&nbsp;

### Or build the image locally

If you need to **debug** or **modify** this Dockerfile, pull the repository down, make your changes, and run the build locally.

```shell
git clone https://github.com/lukeawyatt/docker-tlauncher.git
cd docker-tlauncher
docker build -t tlauncher .
```

&nbsp;

### Run the Container

To spin up the container from your local image using the Docker CLI, **run** the following command.  You can make some simple modifications here to adjust the mount point of your volume in this line `-v $HOME/.minecraft/:/minecraft` where **$HOME/.minecraft** represents the directory path local to your machine.  Note, the volume `-v /tmp/.X11-unix:/tmp/.X11-unix` is utilized by x11 and required for proper display.  Lastly, the addition of `--device /dev/snd` is meant to mount your sound devices.  This might need some tweaking depending on your setup.  Feel free to submit a PR if you have any further adjustments.

```
docker run \
    --rm -dit \
    --device /dev/snd \
    -v $HOME/.minecraft/:/minecraft \
    -v /tmp/.X11-unix:/tmp/.X11-unix \
    -e DISPLAY=$DISPLAY \
    tlauncher
 ```
