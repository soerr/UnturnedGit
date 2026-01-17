FROM debian:trixie-slim

LABEL author="RestoreMonarchy" maintainer="admin@restoremonarchy.com"

ENV DEBIAN_FRONTEND=noninteractive

RUN apt update \
    && apt upgrade -y \
    && apt install -y curl wget jq unzip git libc6 libc6-dev lib32gcc-s1 lib32stdc++6 ca-certificates \
    && useradd -d /home/container -m container \
    && ln -sf /usr/lib/x86_64-linux-gnu/libdl.so.2 /usr/lib/x86_64-linux-gnu/libdl.so \
    && ln -sf /usr/lib/x86_64-linux-gnu/libdl.so.2 /lib/libdl.so

# Install OpenSSL 1.1 from Debian Bullseye for RocketMod compatibility
RUN echo "deb http://deb.debian.org/debian bullseye main" > /etc/apt/sources.list.d/bullseye.list \
    && apt update \
    && apt install -y libssl1.1 \
    && rm /etc/apt/sources.list.d/bullseye.list \
    && apt update

USER container
ENV USER=container
ENV HOME=/home/container

WORKDIR /home/container

COPY --chmod=755 ./entrypoint.sh /entrypoint.sh
COPY --chmod=755 ./repo-sync.sh /repo-sync.sh

CMD ["/bin/bash", "/entrypoint.sh"]
