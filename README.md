# 支持Systemd的Docker镜像

提供支持 systemd 进程管理的 Docker 镜像，用于需要 systemd 管理的服务容器化场景。


## 支持的发行版

### Debian

构建镜像

```bash
# 构建 Debian 11 镜像 (可选 10, 11, 12等)
export TARGET_OS_VERSION=11
docker build -t jockerdragon/docker-systemd:debian-${TARGET_OS_VERSION:-10} \
    --build-arg TAG=${TARGET_OS_VERSION:-10} \
    -f debian/Dockerfile ./debian
```

运行容器

```bash
docker run -d -it \
    --privileged \
    jockerdragon/docker-systemd:debian-${TARGET_OS_VERSION:-10}
```

### CentOS

#### cgroup v1

构建镜像

```bash
# 构建 CentOS 镜像 (已经在7 版本中测试通过)
export TARGET_OS_VERSION=7
docker build -t jockerdragon/docker-systemd:centos-${TARGET_OS_VERSION:-7}-cgroupv1 \
    --build-arg TAG=${TARGET_OS_VERSION:-7} \
    -f centos/cgroupv1/Dockerfile ./centos/cgroupv1
```

运行容器

```bash
export TARGET_OS_VERSION=7
docker run -it -d \
  --privileged \
  jockerdragon/docker-systemd:centos-${TARGET_OS_VERSION:-7}-cgroupv1
```

#### cgroup v2

```bash
# 构建 CentOS 镜像 (已经在7 版本中测试通过)
export TARGET_OS_VERSION=7
docker build -t jockerdragon/docker-systemd:centos-${TARGET_OS_VERSION:-7}-cgroupv2 \
    --build-arg TAG=${TARGET_OS_VERSION:-7} \
    -f centos/cgroupv2/Dockerfile ./centos/cgroupv2
```

运行容器

```bash
export TARGET_OS_VERSION=7
docker run -it -d \
  --privileged \
  jockerdragon/docker-systemd:centos-${TARGET_OS_VERSION:-7}-cgroupv2
```

### RockyLinux

```bash
# 构建 rockylinux 镜像 (可选 - 8 版本中测试通过)
export TARGET_OS_VERSION=8
docker build -t jockerdragon/docker-systemd:rockylinux-${TARGET_OS_VERSION:-8} \
    --build-arg TAG=${TARGET_OS_VERSION:-8} \
    -f rockylinux/Dockerfile ./rockylinux
```

运行容器

```bash
export TARGET_OS_VERSION=8
docker run -it -d \
  --privileged \
  jockerdragon/docker-systemd:rockylinux-${TARGET_OS_VERSION:-8}
```

### Ubuntu

构建镜像

```bash
# 构建 Ubuntu 24.04 镜像 (请选择双数版本，如 20.04, 22.04, 24.04, 26.04 等)
export TARGET_OS_VERSION=24.04
docker build -t jockerdragon/docker-systemd:ubuntu-${TARGET_OS_VERSION:-24.04} \
    --build-arg TAG=${TARGET_OS_VERSION:-24.04} \
    -f ubuntu/Dockerfile ./ubuntu
```

运行容器

```bash
export TARGET_OS_VERSION=24.04
docker run -d -it \
    --privileged \
    jockerdragon/docker-systemd:ubuntu-${TARGET_OS_VERSION:-24.04}
```

## 在其他系统运行

### macOS

由于 macOS 上的 Docker Desktop 使用虚拟机运行容器，需要额外配置 cgroup 支持：

启用 cgroup 挂载（适用于 Docker Desktop 4.3+）：

```bash
# 创建或编辑 ~/.docker/daemon.json
{
  "features": {
    "cgroupv2": true
  }
}
```

重启 Docker Desktop 使配置生效

## 注意事项

1. 可以通过添加 `--cap-add SYS_ADMIN` 能力不需要添加 `--privileged` 特权模式以提高安全性，这种方法还需要挂载 cgroup 文件系统：`-v /sys/fs/cgroup:/sys/fs/cgroup:ro` 。
2. 权限充足情况下可以使用 `--privileged` 特权模式
