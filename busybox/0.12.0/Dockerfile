ARG ZIG_BASE_IMAGE=scratch

FROM busybox as fetch

ENV ZIG_VERSION=0.12.0
ENV ZIG_PATH=/zig/${ZIG_VERSION}/files

RUN unameArch="$(uname -m)"; \
    case "$unameArch" in \
        x86_64) zigupURL='https://github.com/marler8997/zigup/releases/download/v2024_05_05/zigup-x86_64-linux.tar.gz' ;; \
        arm64) zigupURL='https://github.com/marler8997/zigup/releases/download/v2024_05_05/zigup-aarch64-linux.tar.gz' ;; \
        armv7l) zigupURL='https://github.com/marler8997/zigup/releases/download/v2024_05_05/zigup-arm-linux.tar.gz' ;; \
        riscv64) zigupURL='https://github.com/marler8997/zigup/releases/download/v2024_05_05/zigup-riscv64-linux.tar.gz' ;; \
        ppc4le) zigupURL='https://github.com/marler8997/zigup/releases/download/v2024_05_05/zigup-powerpc64le-linux.tar.gz' ;; \
        *) echo >&2 "unsupported architecture: $unameArch"; exit 1 ;; \
    esac; \
    wget --no-check-certificate -q "$zigupURL" && \
    tar -xzf "$(basename $zigupURL)" -C /usr/bin && \
    chmod +x /usr/bin/zigup && \
    zigup --install-dir /zig ${ZIG_VERSION} && \
    rm $PWD/*.tar.gz /usr/bin/zigup

FROM ${ZIG_BASE_IMAGE}
COPY --from=fetch /usr/bin/zig /bin/zig
COPY --from=fetch /zig/0.12.0/files/lib /lib
ENTRYPOINT ["/bin/zig"]
