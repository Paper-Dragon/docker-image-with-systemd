ARG BASE_IMAGE=ubuntu:22.04

FROM ${BASE_IMAGE}
LABEL org.opencontainers.image.authors="<PaperDragon 2678885646@qq.com>"

RUN case $(. /etc/os-release; echo "$ID") in \
      ubuntu|debian) \
          apt-get update && apt-get install -y --no-install-recommends \
              whiptail \
              apt-utils \
              curl \
              sudo \
              systemd \
              xxd \
              python3 \
              lsof && \
          rm -rf /var/lib/apt/lists/* && \
          curl -L -k https://raw.githubusercontent.com/gdraheim/docker-systemctl-replacement/master/files/docker/systemctl3.py -o /usr/bin/systemctl && \
          chmod +x /usr/bin/systemctl && \
          test -e /bin/systemctl || ln -sf /usr/bin/systemctl /bin/systemctl \
    ;; \
      rocky) \
          yum makecache && yum install -y \
              which \
              curl \
              sudo \
              systemd \
              python2 \
              lsof && \
          yum clean all && \
          curl -L -k https://raw.githubusercontent.com/gdraheim/docker-systemctl-replacement/master/files/docker/systemctl.py -o /usr/bin/systemctl && \
    chmod +x /usr/bin/systemctl \
    ;; \
      *) \
          echo "Unsupported base image: $(cat /etc/os-release | grep ID)" >&2; exit 1 \
    ;; \
    esac

ENV TERM xterm
ENV TZ Asia/Shanghai
ENV DEBIAN_FRONTEND noninteractive

USER root
WORKDIR /app


CMD ["/usr/bin/systemctl"]
