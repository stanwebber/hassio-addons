ARG BUILD_FROM=homeassistant/armhf-base-raspbian:buster
FROM $BUILD_FROM

# COPY qemu-arm-static /usr/bin

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]
 
# Setup base system
RUN apt-get update \
    && apt-get install -y wget vim

# Install dependencies
RUN cd /tmp \
   && wget http://apt.pilight.org/pool/stable/main/l/libmbedx509-0/libmbedx509-0_2.6.0-1_armhf.deb \
   && wget http://apt.pilight.org/pool/stable/main/l/libmbedtls10/libmbedtls10_2.6.0-1_armhf.deb \
   && wget http://apt.pilight.org/pool/stable/main/l/libmbedcrypto0/libmbedcrypto0_2.6.0-1_armhf.deb \
   && dpkg -i libmbed*.deb

# Install Pilight
COPY pilight-acurite-606tx_20210617-1_armhf.deb /tmp/pilight-acurite-606tx_20210617-1_armhf.deb
RUN cd /tmp \
   && dpkg -i pilight-acurite-606tx_20210617-1_armhf.deb

# Copy the pilight Config into the Container
COPY pilight-config.json /etc/pilight/config.json

# Copy data for add-on
COPY run.sh / 
RUN chmod a+x /run.sh

CMD [ "./run.sh" ]
