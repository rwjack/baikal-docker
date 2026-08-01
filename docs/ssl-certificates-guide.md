# SSL Certificates Guide

## Let's Encrypt + Traefik

[Traefik](https://traefik.io/) is a modern HTTP reverse proxy that supports Docker + [Let's Encrypt](https://letsencrypt.org) and manages its configuration automatically and dynamically.

An example for Docker Compose can be found at [examples/docker-compose.ssl.yaml](https://github.com/rwjack/baikal-docker/blob/main/examples/docker-compose.ssl.yaml).

This is the recommended approach: other containers can be added easily, and Traefik creates and renews certificates as needed. Traefik itself is an [official Docker image](https://hub.docker.com/_/traefik/).

For more details, see [Traefik's Docker](https://doc.traefik.io/traefik/providers/docker/) and [Traefik's Let's Encrypt](https://doc.traefik.io/traefik/https/acme/) docs.

## Static Certificates

If you want to use your own certificates, hide this container behind your own HTTPS proxy, e.g. with [Traefik's Static Certificates](https://docs.traefik.io/configuration/entrypoints/#static-certificates) or [nginx](https://hub.docker.com/_/nginx/).

This image listens on HTTP port `80` only; terminate TLS at the reverse proxy.
