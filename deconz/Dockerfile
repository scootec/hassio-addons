ARG BUILD_FROM
FROM $BUILD_FROM

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Install deCONZ dependencies
ARG BUILD_ARCH
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    curl \
    kmod \
    lsof \
    tzdata \
    netcat \
    nginx \
    libcap2-bin \
    libqt5core5a \
    libqt5gui5 \
    libqt5network5 \
    libqt5serialport5 \
    libqt5sql5 \
    libqt5websockets5 \
    libqt5widgets5 \
    sqlite3 \
    iputils-ping \
    iproute2 \
    wget \
    && rm -rf /var/lib/apt/lists/*

# Install deCONZ
ARG DECONZ_VERSION
RUN if [ "${BUILD_ARCH}" = "armhf" ]; \
    then \
    curl -q -L -o /deconz.deb http://deconz.dresden-elektronik.de/raspbian/beta/deconz-${DECONZ_VERSION}-qt5.deb; \
    elif [ "${BUILD_ARCH}" = "aarch64" ]; \
    then \
    curl -q -L -o /deconz.deb http://deconz.dresden-elektronik.de/raspbian/alpha/deconz_${DECONZ_VERSION}-debian-stretch-beta_arm64.deb; \
    else \
    curl -q -L -o /deconz.deb http://deconz.dresden-elektronik.de/ubuntu/beta/deconz-${DECONZ_VERSION}-qt5.deb; \
    fi \
    && dpkg --force-all -i /deconz.deb \
    && rm -f /deconz.deb \
    && chown root:root /usr/bin/deCONZ* \
    && sed -i 's/\/root/\/data/' /etc/passwd

COPY rootfs /
