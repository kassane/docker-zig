ARG IMAGE=alpine
ARG BASE_VERSION=latest

FROM ${IMAGE}:${BASE_VERSION}

ENV ZIG_VERSION=master
ENV ZIG_PATH=/zig/${ZIG_VERSION}/files

RUN apk add --no-cache \
        ca-certificates \
        sudo \
        wget

RUN apkArch="$(apk --print-arch)"; \
    case "$apkArch" in \
        x86_64) zigupURL='https://github.com/kassane/zigup/releases/download/2024_03_05/zigup.ubuntu-latest-x86_64.zip' ;; \
        aarch64) zigupURL='https://github.com/kassane/zigup/releases/download/2024_03_05/zigup.ubuntu-latest-aarch64.zip' ;; \
        armv7) zigupURL='https://github.com/kassane/zigup/releases/download/2024_03_05/zigup.ubuntu-latest-armv7a.zip' ;; \
        ppc64le) zigupURL='https://github.com/kassane/zigup/releases/download/2024_03_05/zigup.ubuntu-latest-powerpc64le.zip' ;; \
        *) echo >&2 "unsupported architecture: $apkArch"; exit 1 ;; \
    esac; \
    wget -q "$zigupURL" && \
    unzip -q "$(basename $zigupURL)" -d /usr/bin && \
    chmod +x /usr/bin/zigup && \
    zigup --install-dir /zig ${ZIG_VERSION} \
    && chmod -R a+w ${ZIG_PATH} \
    && rm $PWD/*.zip \
    /usr/bin/zigup; \
    mkdir /app

WORKDIR /app

ARG UNAME=ziguana
ARG UID=1000
ARG GID=1000
RUN addgroup -S $UNAME
RUN adduser \
    --disabled-password \
    --gecos "" \
    --home "$(pwd)" \
    --ingroup "$UNAME" \
    --no-create-home \
    --uid "$UID" \
    "$UNAME"
RUN echo "$UNAME ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/$UNAME \
        && chmod 0440 /etc/sudoers.d/$UNAME

RUN chown -R $UNAME:$UNAME /app

USER $UNAME
