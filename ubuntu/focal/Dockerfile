FROM ubuntu:focal
LABEL org.opencontainers.image.authors="m@rvinvogt.com"

ENV TZ=Europe/Berlin
ENV LC_ALL=C
ENV DEBIAN_FRONTEND=noninteractive
VOLUME [ "/sys/fs/cgroup" ]
CMD ["/sbin/init"]

# hadolint ignore=DL3008
RUN apt-get update && apt-get install --no-install-recommends -y \
    apt-transport-https \
    ca-certificates \
    gnupg2 \
    python3 \
    sudo \
    systemd \
    systemd-sysv \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN rm -f /lib/systemd/system/multi-user.target.wants/* \
    /etc/systemd/system/*.wants/* \
    /lib/systemd/system/local-fs.target.wants/* \
    /lib/systemd/system/sockets.target.wants/*udev* \
    /lib/systemd/system/sockets.target.wants/*initctl* \
    /lib/systemd/system/sysinit.target.wants/systemd-tmpfiles-setup* \
    /lib/systemd/system/systemd-update-utmp*
