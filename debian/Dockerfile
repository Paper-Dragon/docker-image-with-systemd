ARG TAG=10
FROM debian:${TAG}

LABEL org.opencontainers.image.authors="<PaperDragon 2678885646@qq.com>"

ENV container=docker
ENV DEBIAN_FRONTEND=noninteractive


RUN apt-get update && \
    apt-get install -y systemd && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN find /etc/systemd/system \
    /lib/systemd/system \
    -path '*.wants/*' \
    -not -name '*journald*' \
    -not -name '*systemd-tmpfiles*' \
    -not -name '*systemd-user-sessions*' \
    -print0 | xargs -0 rm -vf

ENTRYPOINT [ "/lib/systemd/systemd" ]