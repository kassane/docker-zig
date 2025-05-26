FROM debian:bullseye-slim

ENV ZIG_VERSION=master
ENV ZIG_PATH=/zig/${ZIG_VERSION}/files

RUN apt update && apt install -y --no-install-recommends \
        wget \
        ca-certificates \
        xz-utils

RUN dpkgArch="$(dpkg --print-architecture)"; \
    case "${dpkgArch##*-}" in \
        amd64) zigupURL='https://github.com/marler8997/zigup/releases/download/v2025_05_24/zigup-x86_64-linux.tar.gz' ;; \
        armhf) zigupURL='https://github.com/marler8997/zigup/releases/download/v2025_05_24/zigup-arm-linux.tar.gz' ;; \
        arm64) zigupURL='https://github.com/marler8997/zigup/releases/download/v2025_05_24/zigup-aarch64-linux.tar.gz' ;; \
        riscv64) zigupURL='https://github.com/marler8997/zigup/releases/download/v2025_05_24/zigup-riscv64-linux.tar.gz' ;; \
        ppc64) zigupURL='https://github.com/marler8997/zigup/releases/download/v2025_05_24/zigup-powerpc-linux.tar.gz' ;; \
        ppc64el) zigupURL='https://github.com/marler8997/zigup/releases/download/v2025_05_24/zigup-powerpc64le-linux.tar.gz' ;; \
        i386) echo >&2 "unsupported architecture: ${dpkgArch}"; exit 1 ;; \
        *) echo >&2 "unsupported architecture: ${dpkgArch}"; exit 1 ;; \
    esac; \
    wget -q "$zigupURL" && \
    tar -xzf "$(basename $zigupURL)" -C /usr/bin && \
    chmod +x /usr/bin/zigup && \
    zigup --install-dir /zig ${ZIG_VERSION}

RUN chmod +x ${ZIG_PATH}/zig

RUN apt autoclean \
    && apt remove -y --auto-remove \
        wget \
        ca-certificates \
        xz-utils \
        ; \
    rm /*.tar.gz \
    /usr/bin/zigup; \
    rm -rf /var/lib/apt/lists/*;
