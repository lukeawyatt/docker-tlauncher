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

---

&nbsp;

### Environment Prerequisites:

Prior to running this image, you'll need to ***permit*** Docker on the local machine to connect to the X window display.  Run this command to do so:

```shell
xhost +local:docker
```

&nbsp;

### Build the image from GitHub:

You can build this image directly from GitHub.  This scenario can be utilized when no changes to the image are required.

```shell
docker build -t tlauncher https://github.com/lukeawyatt/docker-tlauncher.git#main:source
```

&nbsp;

### Or build the image locally:

If you need to **debug** or **modify** this Dockerfile, pull the repository down, make your changes, and run the build locally.

```shell
git clone https://github.com/lukeawyatt/docker-tlauncher.git
cd docker-tlauncher/source
docker build -t tlauncher .
```

&nbsp;

### Run the Container:

To spin up the container from your local image using the Docker CLI, **run** the following command.  You can make some simple modifications here to adjust the mount point of your volume in this line `-v $HOME/.minecraft/:/minecraft` where **$HOME/.minecraft** represents the directory path local to your machine.  Note, the volume `-v /tmp/.X11-unix:/tmp/.X11-unix` is utilized by x11 and required for proper display.  There are a few audio options in which you might need to experiment with to get working properly.  See the next section for some suggestions.

```
docker run \
    --rm -dit \
    --device /dev/snd \
    -v $HOME/.minecraft/:/minecraft \
    -v /tmp/.X11-unix:/tmp/.X11-unix \
    -e DISPLAY=$DISPLAY \
    tlauncher
 ```

&nbsp;

### Audio:

Docker Container Audio is hands-down the most finicky portion of this whole process.  If you're not too familiar with how your audio is setup on your local machine, try the **ALSA CONFIGURATION** first and move forward from there.  Feel free to submit a PR if you've discovered any adjustments that have worked with your particular setup.  My personal machine works well with the **PULSEAUDIO CONFIGURATION**.

> **ALSA CONFIGURATION**: Add to docker run
> 
> ```dockerfile
> --device /dev/snd
> ```

&nbsp;

> **PULSEAUDIO CONFIGURATION**: Add to docker run
> 
> ```dockerfile
> --volume /run/user/$(id -u)/pulse/native:/run/user/$(id -u)/pulse/native
> --env PULSE_SERVER=unix:/run/user/$(id -u)/pulse/native
> --user $(id -u):$(id -g)
> ```

&nbsp;

---

&nbsp;

### Next Action:

* Account for java versioning requirements (8, 11, 17)
* Figure out the state of GPU support (I'm personally behind on this understanding)
