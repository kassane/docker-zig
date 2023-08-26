ARG ZIG_BASE_IMAGE=scratch

FROM busybox as fetch

ENV ZIG_VERSION=0.11.0
ENV ZIG_PATH=/zig/${ZIG_VERSION}/files

RUN wget -q https://github.com/marler8997/zigup/releases/download/v2023_07_27/zigup.ubuntu-latest-$(uname -m).zip && \
    unzip zigup.ubuntu-latest-$(uname -m).zip -d /usr/bin \
    && chmod +x /usr/bin/zigup \
    && zigup --install-dir /zig $ZIG_VERSION \
    && chmod -R a+w ${ZIG_PATH} \
    && rm zigup.ubuntu-latest-$(uname -m).zip /usr/bin/zigup

FROM ${ZIG_BASE_IMAGE}
COPY --from=fetch /usr/bin/zig /bin/zig
COPY --from=fetch /zig/0.11.0/files/lib /lib
ENTRYPOINT ["/bin/zig"]
