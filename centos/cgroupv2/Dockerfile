ARG TAG=7
FROM centos:${TAG}

LABEL org.opencontainers.image.authors="<PaperDragon 2678885646@qq.com>"
ENV container=docker

RUN curl -sSL https://www.geekery.cn/sh/LinuxCTS/os/yum/clean_and_set_mirror_centos7.sh | bash
RUN curl https://copr.fedorainfracloud.org/coprs/jsynacek/systemd-backports-for-centos-7/repo/epel-7/jsynacek-systemd-backports-for-centos-7-epel-7.repo > /etc/yum.repos.d/jsynacek-systemd-centos-7.repo && \
    yum update systemd -y && \
    yum clean all

CMD ["/usr/lib/systemd/systemd"]
