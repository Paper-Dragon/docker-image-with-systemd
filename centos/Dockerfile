ARG TAG=7
FROM centos:${TAG}
MAINTAINER paper-dragon 2678885646@qq.com
ENV container docker

RUN yum repolist; yum clean all

RUN yum -y swap -- remove systemd-container systemd-container-libs -- install systemd systemd-libs dbus

RUN systemctl mask dev-mqueue.mount dev-hugepages.mount \
    systemd-remount-fs.service sys-kernel-config.mount \
    sys-kernel-debug.mount sys-fs-fuse-connections.mount \
    display-manager.service graphical.target systemd-logind.service

ADD dbus.service /etc/systemd/system/dbus.service
RUN ln -s /usr/lib/systemd/system/dbus.service /etc/systemd/system/multi-user.target.wants/dbus.service


#RUN yum -y install passwd; yum clean all
#RUN echo root | passwd --stdin root

#RUN yum -y install openssh-server initscripts; yum clean all
#RUN echo "UseDNS no" >> /etc/ssh/sshd_config
#RUN sed -i 's/UsePrivilegeSeparation sandbox/UsePrivilegeSeparation no/' /etc/ssh/sshd_config

VOLUME ["/sys/fs/cgroup"]
VOLUME ["/run"]

CMD  ["/usr/lib/systemd/systemd"]