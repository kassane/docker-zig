FROM debian:bullseye-slim

ENV ZIG_VERSION=master
ENV ZIG_PATH=/zig/${ZIG_VERSION}/files

RUN apt update && apt install -y --no-install-recommends \
        wget \
        ca-certificates \
        unzip \
        xz-utils

RUN dpkgArch="$(dpkg --print-architecture)"; \
    case "${dpkgArch##*-}" in \
        amd64) zigupURL='https://github.com/kassane/zigup/releases/download/2023_09_29/zigup.ubuntu-latest-x86_64.zip' ;; \
        armhf) zigupURL='https://github.com/kassane/zigup/releases/download/2023_09_29/zigup.ubuntu-latest-armv7a.zip' ;; \
        arm64) zigupURL='https://github.com/kassane/zigup/releases/download/2023_09_29/zigup.ubuntu-latest-aarch64.zip' ;; \
        riscv64) zigupURL='https://github.com/kassane/zigup/releases/download/2023_09_29/zigup.ubuntu-latest-riscv64.zip' ;; \
        ppc64) zigupURL='https://github.com/kassane/zigup/releases/download/2023_09_29/zigup.ubuntu-latest-powerpc.zip' ;; \
        ppc64el) zigupURL='https://github.com/kassane/zigup/releases/download/2023_09_29/zigup.ubuntu-latest-powerpc64le.zip' ;; \
        i386) echo >&2 "unsupported architecture: ${dpkgArch}"; exit 1 ;; \
        *) echo >&2 "unsupported architecture: ${dpkgArch}"; exit 1 ;; \
    esac; \
    wget -q "$zigupURL" && \
    unzip -q "$(basename $zigupURL)" -d /usr/bin && \
    chmod +x /usr/bin/zigup && \
    zigup --install-dir /zig ${ZIG_VERSION}

RUN chmod +x ${ZIG_PATH}/zig

RUN apt autoclean \
    && apt remove -y --auto-remove \
        wget \
        ca-certificates \
        unzip \
        xz-utils \
        ; \
    rm /*.zip \
    /usr/bin/zigup; \
    rm -rf /var/lib/apt/lists/*;
