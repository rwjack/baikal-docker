# Unraid Docker Baikal Installation Guide

Install Baikal on [Unraid](https://unraid.net/) from the GitHub Container Registry image `ghcr.io/rwjack/baikal`. Many thanks to [@Joshndroid](https://github.com/Joshndroid) for the original guide.

## Prerequisites

1. Docker enabled in Unraid (see [Docker Management](https://wiki.unraid.net/Manual/Docker_Management))
1. (Optional) A reverse proxy container and network for TLS

**Installation Note** – Available tags are listed in the [README](https://github.com/rwjack/baikal-docker#supported-tags). Recommended pin: `ghcr.io/rwjack/baikal:0.11.1`.

**Further Installation Note** – If you use an external database such as [MariaDB](https://hub.docker.com/_/mariadb), ensure Baikal and the database can connect (same Docker network; DB user created ahead of time).

## Installation

1. In Unraid, go to **Docker** → **Add Container**.

1. Set **Repository** to `ghcr.io/rwjack/baikal:0.11.1` (or another tag from the README).

1. Switch from _Basic View_ to _Advanced View_.

1. Set **Icon URL** to <https://raw.githubusercontent.com/sabre-io/sabre.io/master/source/img/baikal.png>.

1. Set **WebUI** to `http://[IP]:[PORT:80]/`.

1. Set **Extra Parameters** to `--restart=always`.

1. (Optional) Set network type to match your reverse proxy network.

1. Add a path:
   - Name: `Config`
   - Container Path: `/var/www/baikal/config`
   - Host Path: `/mnt/user/appdata/baikal/config`
   - Access Mode: `Read/Write`

1. Add a path:
   - Name: `Specific`
   - Container Path: `/var/www/baikal/Specific`
   - Host Path: `/mnt/user/appdata/baikal/specific`
   - Access Mode: `Read/Write`

1. Add a port:
   - Container Port: `80`
   - Host Port: `80` (or another free host port)
   - Connection Type: `TCP`

1. Click **Apply**, start the container, then open the WebUI and complete Baikal setup.

1. (Optional) Point your reverse proxy at the Baikal host port for HTTPS.
