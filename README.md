# Baikal Docker

Ready-to-go [Baikal](https://sabre.io/baikal/) CalDAV/CardDAV server images (nginx + PHP).

[![Rebuild images](https://github.com/rwjack/baikal-docker/actions/workflows/build-latest.yaml/badge.svg)](https://github.com/rwjack/baikal-docker/actions/workflows/build-latest.yaml)
[![Build release images](https://github.com/rwjack/baikal-docker/actions/workflows/build-release.yaml/badge.svg)](https://github.com/rwjack/baikal-docker/actions/workflows/build-release.yaml)
[![Testing images](https://github.com/rwjack/baikal-docker/actions/workflows/build-testing.yaml/badge.svg)](https://github.com/rwjack/baikal-docker/actions/workflows/build-testing.yaml)
![Docker Architectures](https://img.shields.io/badge/arch-amd64%20%7C%20arm32v7%20%7C%20arm64v8-informational)

## Credits

Based on the excellent work of:

- **[ckulka/baikal-docker](https://github.com/ckulka/baikal-docker)** — original Docker image, compose examples, and docs
- **[aalmenar/baikal-docker](https://github.com/aalmenar/baikal-docker)** — Baikal 0.11.x bump, PHP 8.5, nginx-default packaging, and related fixes

This repository continues that lineage with clearer version tagging and scheduled package rebuilds.

## Supported tags

Images are published to `ghcr.io/rwjack/baikal` (nginx only).

| Tag | Meaning |
| --- | --- |
| `0.11.1` | Current Baikal release; rebuilt on the 1st and 15th with fresh OS/PHP packages |
| `0.11.1-YYYYMMDD` | Pin to a specific release or scheduled rebuild (UTC date) |
| `latest` | Alias of the current version tag after each release/rebuild |
| `testing` | Built from the `testing` branch; for pre-release validation |

Version naming follows [Baikal](https://sabre.io/baikal/) itself. Multi-arch: `amd64`, `arm32v7`, `arm64v8`.

Dockerfile: [`nginx.dockerfile`](nginx.dockerfile) (currently Baikal `0.11.1`).

## Quick reference

- **Issues**: https://github.com/rwjack/baikal-docker/issues
- **PRs**: https://github.com/rwjack/baikal-docker/pulls
- **Source**: https://github.com/rwjack/baikal-docker

## What is Baikal?

From [sabre.io/baikal](https://sabre.io/baikal/):

> Baikal is a Cal and CardDAV server, based on sabre/dav, that includes an administrative interface for easy management.

## How to use this image

```bash
docker run --rm -it -p 80:80 ghcr.io/rwjack/baikal:0.11.1
```

Or use [examples/docker-compose.yaml](examples/docker-compose.yaml):

```bash
docker compose -f examples/docker-compose.yaml up
```

Open http://localhost (or your host IP) in a browser.

### Persistent data

The image exposes `/var/www/baikal/Specific` and `/var/www/baikal/config`. Back these up regularly.

For bind mounts instead of named volumes, see [examples/docker-compose.localvolumes.yaml](examples/docker-compose.localvolumes.yaml).

On start, `/docker-entrypoint.d/40-fix-baikal-file-permissions.sh` fixes ownership. Disable with `BAIKAL_SKIP_CHOWN=true`.

### Guides

- [Email Guide](docs/email-guide.md)
- [Home Assistant Fix](docs/home-assistant-fix.md)
- [SSL Certificate Guide](docs/ssl-certificates-guide.md)
- [systemd Guide](docs/systemd-guide.md)
- [Unraid Installation Guide](docs/unraid-installation-guide.md)

## Image variants

### `ghcr.io/rwjack/baikal:0.11.1`

Recommended pin. Same Baikal version across rebuilds; OS and PHP packages stay current via the bi-monthly rebuild workflow. Each release and scheduled rebuild also publishes `0.11.1-YYYYMMDD`.

### `ghcr.io/rwjack/baikal:latest`

Floating alias of the current release, updated on releases and scheduled rebuilds.

### `ghcr.io/rwjack/baikal:testing`

Built from the `testing` branch on every push/merge. Use this to validate Dockerfile or packaging changes before cutting a version release on `main`.
