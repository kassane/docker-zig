# Docker-Zig

**DockerHub:** https://hub.docker.com/repositories/kassany

Minimal Container to use Zig toolchain. Downloaded by [zigup](https://github.com/marler8997/zigup) (Thx [@marler8997](https://github.com/marler8997))

#### Tags = version

- `latest`: `master`
- `0.11.0`: `0.11.0`

```bash
## busybox
docker run --rm -v $(pwd):/app -w /app kassany/ziglang:{tagname}
## debian
docker run --rm -it -v $(pwd):/app -w /app kassany/bookworm-ziglang:{tagname} bash
```
