FROM ghcr.io/home-assistant/base:latest

LABEL \
  io.hass.version="VERSION" \
  io.hass.type="app" \
  io.hass.arch="aarch64|amd64"

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

COPY rootfs /

# Install requirements for app
RUN \
  apk add --no-cache --update tar procps-ng python3 nrpe nagios-plugins-all monitoring-plugins \
  && rc-update add nrpe default \
  && ARCH="${BUILD_ARCH}" \
  && if [ "${BUILD_ARCH}" = "aarch64" ]; then ARCH="arm64"; fi

RUN chmod -R 755 /usr/lib/nagios/plugins/

LABEL \
    org.opencontainers.image.title="Home Assistant App: Nagios NRPE" \
    org.opencontainers.image.description="Nagios NRPE Server for monitoring Home Assistant" \
    org.opencontainers.image.source="https://github.com/petrivirkkula/assio-app-nagios-nrpe" \
    org.opencontainers.image.licenses="GNU Public License v3.0"

#ENTRYPOINT []
RUN chmod a+x /run.sh
CMD [ "/run.sh" ]