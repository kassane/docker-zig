ARG IMAGE=debian
ARG BASE_VERSION=latest
ARG IMAGE_ARCH=amd64

FROM --platform=linux/${IMAGE_ARCH} ${IMAGE}:${BASE_VERSION}

ENV ZIG_VERSION=0.11.0
ENV ZIG_PATH=/zig/${ZIG_VERSION}/files

RUN apt update && apt install -q -y \
        wget unzip xz-utils

RUN wget -q https://github.com/marler8997/zigup/releases/download/v2023_07_27/zigup.ubuntu-latest-$(uname -m).zip && \
    unzip zigup.ubuntu-latest-$(uname -m).zip -d /usr/bin \
    && chmod +x /usr/bin/zigup \
    && zigup --install-dir /zig ${ZIG_VERSION} \
    && chmod -R a+w ${ZIG_PATH}

ARG UNAME=ziguana
ARG UID=1000
ARG GID=1000
RUN groupadd -g $GID -o $UNAME
RUN useradd -m -u $UID -g $GID -o -s /bin/bash $UNAME

USER $UNAME