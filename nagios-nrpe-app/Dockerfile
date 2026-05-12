FROM ghcr.io/home-assistant/base:latest

LABEL \
  io.hass.version="VERSION" \
  io.hass.type="app" \
  io.hass.arch="aarch64|amd64"

 COPY rootfs /

# Install requirements for app
RUN \
  apk add --no-cache --update tar procps-ng python3 nrpe nagios-plugins-all monitoring-plugins \
  && rc-update add nrpe default \
  && ARCH="${BUILD_ARCH}" \
  && if [ "${BUILD_ARCH}" = "aarch64" ]; then ARCH="arm64"; fi
# Copy data for app
RUN chmod -R 755 /usr/lib/nagios/plugins/
ENTRYPOINT []
COPY run.sh /
RUN chmod a+x /run.sh
CMD [ "/run.sh" ]