# run centos in un privilege mode

```bash
docker run -it --rm \
  -v /sys/fs/cgroup:/sys/fs/cgroup:ro \
  jockerdragon/centos-systemd:7
```

```bash
docker run -it --rm \
  --privileged \
  jockerdragon/centos-systemd:7
```
