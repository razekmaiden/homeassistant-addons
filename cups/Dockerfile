ARG BUILD_FROM
FROM $BUILD_FROM

LABEL io.hass.version="1" io.hass.type="addon" io.hass.arch="armhf|aarch64|i386|amd64"

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        cups \
        avahi-daemon \
        libnss-mdns \
        dbus \
        colord \
        printer-driver-all-enforce \
        openprinting-ppds \
        hpijs-ppds \
        hp-ppd  \
        hplip \
        gnupg2 \
        lsb-release \
        nano \
        samba \
        bash-completion \
        nginx \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*
# Install drivers for brother dcpt300
RUN wget https://download.brother.com/welcome/dlf101960/dcpt300lpr-3.0.2-0.i386.deb && \
    dpkg -i --force-all dcpt300lpr-3.0.2-0.i386.deb

RUN wget https://download.brother.com/welcome/dlf101961/dcpt300cupswrapper-3.0.2-0.i386.deb && \
    dpkg -i --force-all dcpt300cupswrapper-3.0.2-0.i386.deb
COPY rootfs /

# Corrects permissions for s6 v3
RUN if [ -d /etc/cont-init.d ]; then chmod -R 755 /etc/cont-init.d; fi && \
    if [ -d /etc/services.d ]; then chmod -R 755 /etc/services.d; fi && \
    if [ -f /entrypoint.sh ]; then chmod 755 /entrypoint.sh; fi

EXPOSE 631 445 137 139

RUN chmod a+x /run.sh
CMD ["/run.sh"]
