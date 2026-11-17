# Homelab

Public write-up of my Proxmox homelab: an automated media server, a dev/test box for self-hosted apps, and a game server VM. Compose files for the media server are in this repo, ready to adapt.

> Architecture diagram: _being redrawn_.

## Overview

One Proxmox host runs two Ubuntu LXC containers and one Ubuntu VM.

| Guest | Type | Purpose | Docs |
|---|---|---|---|
| `media-server` | LXC (Ubuntu, Docker + Portainer) | Fully automated media pipeline: request, download, process, stream | [media-server/](media-server/) |
| `web-test` | LXC (Ubuntu, Docker + Portainer) | Staging and self-hosted apps unrelated to media | [dev-test/](dev-test/) |
| `pelican-panel` | VM (Ubuntu) | Game servers: Pelican Panel + Wings | [game-servers/](game-servers/) |

Host hardware, resource allocation and storage are in [docs/proxmox.md](docs/proxmox.md).

## Repository layout

```
.
├── README.md
├── docs/
│   └── proxmox.md                    host hardware, guests, storage
├── media-server/
│   ├── README.md                     how the automation pipeline works
│   ├── media-management-stack.yaml   Plex, Overseerr, Wizarr, Tautulli, Threadfin, FileFlows
│   ├── torrent-stack.yaml            gluetun VPN, qBittorrent, Sonarr, Radarr, Prowlarr, Bazarr, ...
│   ├── .env.media-stack.example
│   └── .env.torrent-stack.example
├── dev-test/
│   └── README.md                     apps hosted on the dev/test LXC
└── game-servers/
    └── README.md                     Pelican Panel + Wings VM
```

## Quick start (media server)

```bash
cd media-server
cp .env.torrent-stack.example .env.torrent-stack   # fill in VPN keys, paths
cp .env.media-stack.example   .env.media-stack
docker compose --env-file .env.torrent-stack -f torrent-stack.yaml up -d
docker compose --env-file .env.media-stack   -f media-management-stack.yaml up -d
```

Real `.env.*` files are git-ignored; only the `.example` files are committed. In Portainer, paste the compose file into a stack and enter the variables in its environment section.
