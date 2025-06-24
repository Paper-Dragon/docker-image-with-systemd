ARG TAG=22.04
FROM ubuntu:${TAG}
LABEL org.opencontainers.image.authors="<PaperDragon 2678885646@qq.com>"

ENV container=docker

# Don't start any optional services except for the few we need.
#RUN find /etc/systemd/system \
#    /lib/systemd/system \
#    -path '*.wants/*' \
#    -not -name '*journald*' \
#    -not -name '*systemd-tmpfiles*' \
#    -not -name '*systemd-user-sessions*' \
#    -exec rm \{} \;

RUN apt-get update && \
    apt-get install -y systemd && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN systemctl set-default multi-user.target

STOPSIGNAL SIGRTMIN+3

CMD ["/lib/systemd/systemd"]