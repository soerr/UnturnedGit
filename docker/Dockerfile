FROM debian:trixie-slim

LABEL author="RestoreMonarchy" maintainer="admin@restoremonarchy.com"

ENV DEBIAN_FRONTEND=noninteractive

RUN apt update \
    && apt upgrade -y \
    && apt install -y curl wget jq unzip git libc6 libc6-dev lib32gcc-s1 lib32stdc++6 \
    && useradd -d /home/container -m container \
    && ln -sf /usr/lib/x86_64-linux-gnu/libdl.so.2 /usr/lib/x86_64-linux-gnu/libdl.so \
    && ln -sf /usr/lib/x86_64-linux-gnu/libdl.so.2 /lib/libdl.so

USER container
ENV USER=container
ENV HOME=/home/container

WORKDIR /home/container

COPY ./entrypoint.sh /entrypoint.sh
COPY ./repo-sync.sh /repo-sync.sh

CMD ["/bin/bash", "/entrypoint.sh"]
