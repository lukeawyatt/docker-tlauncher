###############################################################################################################################
##                                                                                                                           ##
##  ███    ███ ██ ███    ██ ███████  ██████ ██████   █████  ███████ ████████                                                 ##
##  ████  ████ ██ ████   ██ ██      ██      ██   ██ ██   ██ ██         ██                                                    ##
##  ██ ████ ██ ██ ██ ██  ██ █████   ██      ██████  ███████ █████      ██                                                    ##
##  ██  ██  ██ ██ ██  ██ ██ ██      ██      ██   ██ ██   ██ ██         ██                                                    ##
##  ██      ██ ██ ██   ████ ███████  ██████ ██   ██ ██   ██ ██         ██                                                    ##
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

# BASE IMAGE: DEBIAN
FROM docker.io/debian

# LAYER 1: REQUIREMENTS
RUN apt-get update && \
    apt-get upgrade && \
    apt-get install -y jq curl procps fonts-dejavu openjdk-17-jre openjfx default-jdk x11-xserver-utils unzip

# LAYER 2: CREATE USER
RUN useradd -d /minecraft -s /bin/sh minecraft

# LAYER 3: DOWNLOAD AND INSTALL TLAUNCHER
RUN mkdir -p /opt/tlauncher && \
    curl -sL "https://tlauncher.org/jar" -o '/opt/tlauncher/tlauncher.zip' && \
    unzip /opt/tlauncher/tlauncher.zip -d /opt/tlauncher && \
    chown minecraft:minecraft -R /opt/tlauncher && \
    mv /opt/tlauncher/TLauncher-2.841.jar /opt/tlauncher/tlauncher.jar

# LAYER 4: CLEANUP
RUN apt-get remove -y unzip curl

# LAYER 5: SPECIFY USER
USER minecraft

# CONTAINER ENTRYPOINT: JAVA RUN
ENTRYPOINT java -jar /opt/tlauncher/tlauncher.jar && \
           while :; do [ $(pgrep -f tlauncher | wc -l) -gt 2 ] && sleep 5 || exit 0; done
