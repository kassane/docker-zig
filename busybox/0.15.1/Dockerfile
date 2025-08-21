ARG ZIG_BASE_IMAGE=scratch

FROM busybox as fetch

ENV ZIG_VERSION=0.15.1
ENV ZIG_PATH=/zig/${ZIG_VERSION}/files

# Download CA certificates manually
ADD https://curl.se/ca/cacert.pem /etc/ssl/certs/ca-certificates.crt
ENV SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt

RUN unameArch="$(uname -m)"; \
    case "$unameArch" in \
        x86_64) zigupURL='https://github.com/marler8997/zigup/releases/download/v2025_05_24/zigup-x86_64-linux.tar.gz' ;; \
        arm64) zigupURL='https://github.com/marler8997/zigup/releases/download/v2025_05_24/zigup-aarch64-linux.tar.gz' ;; \
        armv7l) zigupURL='https://github.com/kassane/zigup/releases/download/2024_03_05/zigup-arm-linux.tar.gz' ;; \
        ppc4le) zigupURL='https://github.com/marler8997/zigup/releases/download/v2025_05_24/zigup-powerpc64le-linux.tar.gz' ;; \
        riscv64) zigupURL='https://github.com/marler8997/zigup/releases/download/v2025_05_24/zigup-riscv64-linux.tar.gz' ;; \
        s390x) zigupURL='https://github.com/kassane/zigup/releases/download/2024_03_05/zigup-s390x-linux.tar.gz' ;; \
        *) echo >&2 "unsupported architecture: $unameArch"; exit 1 ;; \
    esac; \
    wget --no-check-certificate -q "$zigupURL" && \
    tar -xzf "$(basename $zigupURL)" -C /usr/bin && \
    chmod +x /usr/bin/zigup && \
    zigup --install-dir /zig ${ZIG_VERSION} && \
    rm $PWD/*.tar.gz /usr/bin/zigup

FROM ${ZIG_BASE_IMAGE}
COPY --from=fetch /usr/bin/zig /bin/zig
COPY --from=fetch /zig/0.15.1/files/lib /lib
ENTRYPOINT ["/bin/zig"]