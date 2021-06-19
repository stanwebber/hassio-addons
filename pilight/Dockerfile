ARG BUILD_FROM=homeassistant/aarch64-base-debian:stretch
FROM $BUILD_FROM

# COPY qemu-arm-static /usr/bin

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]
 
# Setup base system
RUN apt-get update \
    && apt-get install -y wget gnupg \
    && echo "deb http://apt.pilight.org/ stable main" > /etc/apt/sources.list.d/pilight.list \
    && wget -O - http://apt.pilight.org/pilight.key | apt-key add - \

# Install dependencies
    && apt-get update \
    && apt-get install -y libwiringx

# Install Pilight
COPY pilight-acurite-606tx_20210619-1_arm64.deb /tmp/pilight-acurite-606tx_20210619-1_arm64.deb
RUN cd /tmp \
   && dpkg -i pilight-acurite-606tx*.deb \
   && rm -f pilight-acurite-606tx*.deb

# Copy the pilight Config into the Container
COPY pilight-config.json /etc/pilight/config.json

# Copy data for add-on
COPY run.sh / 
RUN chmod a+x /run.sh

CMD [ "./run.sh" ]
