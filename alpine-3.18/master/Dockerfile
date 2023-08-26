ARG IMAGE=alpine
ARG BASE_VERSION=3.18
ARG IMAGE_ARCH=amd64

FROM --platform=linux/${IMAGE_ARCH} ${IMAGE}:${BASE_VERSION}

ENV ZIG_VERSION=master
ENV ZIG_PATH=/zig/${ZIG_VERSION}/files

RUN apk add --no-cache \
        ca-certificates \
        wget

RUN wget -q https://github.com/marler8997/zigup/releases/download/v2023_07_27/zigup.ubuntu-latest-$(uname -m).zip && \
    unzip zigup.ubuntu-latest-$(uname -m).zip -d /usr/bin \
    && chmod +x /usr/bin/zigup \
    && zigup --install-dir /zig ${ZIG_VERSION} \
    && chmod -R a+w ${ZIG_PATH} \
    && rm zigup.ubuntu-latest-$(uname -m).zip \
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

RUN chown -R $UNAME:$UNAME /app

USER $UNAME