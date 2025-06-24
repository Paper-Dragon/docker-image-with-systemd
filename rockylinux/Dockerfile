ARG TAG=8
FROM rockylinux/rockylinux:${TAG}

LABEL org.opencontainers.image.authors="<PaperDragon 2678885646@qq.com>"
ENV container=docker

# RUN INSTALL_PKGS='findutils glibc-common initscripts iproute python3 sudo' \
#     && dnf makecache && dnf install -y $INSTALL_PKGS \
#     && dnf clean all

RUN dnf makecache && \
    dnf install -y findutils systemd \
    && dnf clean all

RUN find /etc/systemd/system /lib/systemd/system \
    -path '*.wants/*' \
    -not -name '*journald*' \
    -not -name '*systemd-tmpfiles*' \
    -not -name '*systemd-user-sessions*' \
    -print0 | xargs -0 rm -vf

CMD ["/usr/lib/systemd/systemd"]
