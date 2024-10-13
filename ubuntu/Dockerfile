ARG TAG=22.04
FROM ubuntu:${TAG}
LABEL org.opencontainers.image.authors="<PaperDragon 2678885646@qq.com>"

ENV container docker

# Don't start any optional services except for the few we need.
#RUN find /etc/systemd/system \
#    /lib/systemd/system \
#    -path '*.wants/*' \
#    -not -name '*journald*' \
#    -not -name '*systemd-tmpfiles*' \
#    -not -name '*systemd-user-sessions*' \
#    -exec rm \{} \;

# For china mainland settings ,change mirrorlist to china mainline
# RUN echo "nameserver 8.8.8.8" > /etc/resolv.conf
RUN sed -i 's/deb.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list

RUN apt-get update && \
    apt-get install -y systemd systemd-sysv && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN systemctl set-default multi-user.target

STOPSIGNAL SIGRTMIN+3

CMD ["/bin/bash", "-c", "exec /sbin/init --log-target=journal 3>&1"]