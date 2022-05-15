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

This project offers a quick way to spin up the TLauncher Minecraft client within a Docker container.  This can be used to 

This repository is derived from [dm9pZCAq's](https://github.com/dm9pZCAq/docker-tlauncher) repository.

&nbsp;

### Environment Prerequisites:

Prior to running this image, you'll need to permit Docker on the local machine to connect to the X window display.  Run this command to do so:

```shell
xhost +local:docker
```

&nbsp;

### Build the image from GitHub

You can build this image directly from GitHub.  This scenario can be utilized when no changes are required.

```
docker build -t tlauncher github.com/lukeawyatt/docker-tlauncher
```

&nbsp;

### Build the image locally

If you need to debug or modify this Dockerfile, pull the repository down, make your changes, and run the build locally.

```
git clone https://github.com/lukeawyatt/docker-tlauncher.git
cd docker-tlauncher
docker build -t tlauncher .
```

&nbsp;

### Run the Container

To spin up the container from your local image using the Docker CLI, run the following command.

```
docker run \
    --rm -dit \
    --device /dev/snd \
    -v $HOME/.minecraft/:/minecraft \
    -v /tmp/.X11-unix:/tmp/.X11-unix \
    -e DISPLAY=$DISPLAY \
    tlauncher
 ```
 