# docker-image-with-systemd
>
> description:
>
> docker images add systemd process management tools.



## debian

description:
if u want debian version 10, set TAG=10.

```bash
# default debian version: 10
docker build -t jockerdragon/debian-systemd:10 \
    --build-arg TAG=10 \
    -f debian/Dockerfile .
docker run -d -it                       \
    -v /sys/fs/cgroup:/sys/fs/cgroup:ro \
    --cap-add SYS_ADMIN                 \
    jockerdragon/debian-systemd:10
```

## centos

#### cgroup v1
```bash
docker build -t jockerdragon/centos-systemd:7-cgroupv1 \
    --build-arg TAG=7 \
    -f centos/cgroupv1/Dockerfile ./centos/cgroupv1
    
docker run -it --rm \
  -v /sys/fs/cgroup:/sys/fs/cgroup:ro \
  jockerdragon/centos-systemd:7-cgroupv1

docker run -it --rm \
  --privileged \
  jockerdragon/centos-systemd:7-cgroupv1
```

#### cgroup v2

build centos image (cgroup v2)

```bash
docker build -t jockerdragon/centos-systemd:7-cgroupv2 \
    --build-arg TAG=7 \
    -f centos/cgroupv2/Dockerfile ./centos/cgroupv2
```


run centos image (cgroup v2)

```bash
docker run -it --rm \
  --privileged \
  jockerdragon/centos-systemd:7-cgroupv2

```


## rockylinux

same as centos

## ubuntu

```bash
# default ubuntu version: 22.10
docker build -t jockerdragon/ubuntu-systemd:23.04 \
    --build-arg TAG=23.04 \
    -f ubuntu/Dockerfile ./ubuntu
docker run -d -it                       \
    -v /sys/fs/cgroup:/sys/fs/cgroup:ro \
    --cap-add SYS_ADMIN                 \
    jockerdragon/ubuntu-systemd:23.04
```

## run at other os

### Mac

As the image mounts the systemd cgroup into the container, the host needs to have it mounted already. However, boot2docker doesn't have systemd installed and therefore this cgroup isn't available.
To get the cgroup mounted in the Docker VM, you can login into the VM by running docker-machine ssh and run the following code to apply the patch:

```bash

sudo -s
cat >> /var/lib/boot2docker/bootsync.sh <<EOF
mkdir /sys/fs/cgroup/systemd
mount -t cgroup -o none,name=systemd cgroup /sys/fs/cgroup/systemd
EOF
exit
```

## Thanks

- [asg1612/docker-debian-systemd](https://github.com/asg1612/docker-debian-systemd)
