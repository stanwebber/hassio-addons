ARG BUILD_FROM=homeassistant/aarch64-base-debian:stretch
FROM $BUILD_FROM

# COPY qemu-arm-static /usr/bin

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]
 
# Setup base system
RUN apt-get update \
    && apt-get install -y wget gnupg apt-transport-https \
    && echo "deb http://apt.pilight.org/ stable main" > /etc/apt/sources.list.d/pilight.list \
    && wget -O - http://apt.pilight.org/pilight.key | apt-key add - \
# Install dependencies
    && apt-get update \
    && apt-get install -y libunwind8 libwiringx

# Install Pilight
COPY pilight-acurite-606tx_8.0.2-1_*.deb /tmp/
RUN cd /tmp \
   && if [ "$(uname -m)" = aarch64 ]; \
   then \
     dpkg -i pilight-acurite-606tx_8.0.2-1_arm64.deb; \
   else \
     dpkg -i pilight-acurite-606tx_8.0.2-1_armhf.deb; \
   fi \
   && rm -f pilight-acurite-606tx_8.0.2-1_*.deb

# Copy the pilight Config into the Container
COPY pilight-config.json /etc/pilight/config.json

# Copy data for add-on
COPY run.sh / 
RUN chmod a+x /run.sh

CMD [ "./run.sh" ]
