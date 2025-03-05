# Docker-Zig

**DockerHub:** https://hub.docker.com/u/kassany

Minimal Container to use Zig toolchain. Downloaded by [zigup](https://github.com/marler8997/zigup) (Thx [@marler8997](https://github.com/marler8997))

#### Tags = version

- `latest`: `master`
- `0.11.0`: `0.11.0`
- `0.12.0`: `0.12.0`
- `0.13.0`: `0.13.0`
- `0.14.0`: `0.14.0`

```bash
## busybox (x86_64)
docker run --rm -v $(pwd):/app -w /app kassany/ziglang:{tagname}
## debian (x86_64|ARM64|ARM32v7|PPC64LE)
docker run --rm -it -v $(pwd):/app -w /app kassany/bookworm-ziglang:{tagname} bash
## alpine 3.18 (x86_64|ARM64|ARM32v7|PPC64LE|RISCV64)
docker run --rm -it -v $(pwd):/app -w /app kassany/alpine-ziglang:{tagname} ash
```
