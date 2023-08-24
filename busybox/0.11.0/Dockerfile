ARG ZIG_BASE_IMAGE=scratch

FROM busybox as fetch

ARG ZIG_VERSION=0.11.0
ENV ZIG_VERSION=${ZIG_VERSION}

RUN wget -q https://github.com/marler8997/zigup/releases/download/v2023_07_27/zigup.ubuntu-latest-$(uname -m).zip && \
    unzip zigup.ubuntu-latest-$(uname -m).zip -d /usr/bin && chmod +x /usr/bin/zigup && zigup --install-dir /zig $ZIG_VERSION

FROM ${ZIG_BASE_IMAGE}
COPY --from=fetch /usr/bin/zig /bin/zig
COPY --from=fetch /zig/0.11.0/files/lib /bin/lib
ENTRYPOINT ["/bin/zig"]
