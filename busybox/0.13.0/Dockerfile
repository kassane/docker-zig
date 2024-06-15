ARG ZIG_BASE_IMAGE=scratch

FROM busybox as fetch

ENV ZIG_VERSION=0.13.0
ENV ZIG_PATH=/zig/${ZIG_VERSION}/files

RUN unameArch="$(uname -m)"; \
    case "$unameArch" in \
        x86_64) zigupURL='https://github.com/kassane/zigup/releases/download/2023_09_29/zigup.ubuntu-latest-x86_64.zip' ;; \
        arm64) zigupURL='https://github.com/kassane/zigup/releases/download/2023_09_29/zigup.ubuntu-latest-aarch64.zip' ;; \
        armv7l) zigupURL='https://github.com/kassane/zigup/releases/download/2023_09_29/zigup.ubuntu-latest-armv7a.zip' ;; \
        riscv64) zigupURL='https://github.com/kassane/zigup/releases/download/2023_09_29/zigup.ubuntu-latest-riscv64.zip' ;; \
        ppc4le) zigupURL='https://github.com/kassane/zigup/releases/download/2023_09_29/zigup.ubuntu-latest-powerpc64le.zip' ;; \
        *) echo >&2 "unsupported architecture: $unameArch"; exit 1 ;; \
    esac; \
    wget --no-check-certificate -q "$zigupURL" && \
    unzip -q "$(basename $zigupURL)" -d /usr/bin && \
    chmod +x /usr/bin/zigup && \
    zigup --install-dir /zig ${ZIG_VERSION} && \
    rm $PWD/*.zip /usr/bin/zigup

FROM ${ZIG_BASE_IMAGE}
COPY --from=fetch /usr/bin/zig /bin/zig
COPY --from=fetch /zig/0.13.0/files/lib /lib
ENTRYPOINT ["/bin/zig"]