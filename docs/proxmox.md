# Proxmox host

## Hardware

| | |
|---|---|
| CPU | Intel Core i5-8400 @ 2.80 GHz, 6 cores / 1 socket |
| RAM | ~24 GB (23.39 GiB) |
| Boot / VM storage | 1 TB SATA SSD (LVM), ~94 GiB root |
| Bulk storage | 2 × 8 TB Seagate HDD (ext4) |
| Boot mode | EFI |
| Software | Proxmox VE 9.0, kernel 6.14 (pve) |

## Guests

| Name | Type | OS | vCPU | RAM | Swap | Disk | Privileged |
|---|---|---|---|---|---|---|---|
| `media-server` | LXC | Ubuntu | 6 | 9.78 GiB | 2.94 GiB | ~98 GiB | yes |
| `web-test` | LXC | Ubuntu | 2 | 3.91 GiB | 1.97 GiB | ~49 GiB | yes |
| `pelican-panel` | VM | Ubuntu | 4 | 15.63 GiB | - | 200 GiB | n/a |

Both LXCs run Docker with Portainer for UI management. They are privileged so Docker, `/dev/dri` (Intel iGPU transcoding) and bind-mounted storage work without UID mapping.

## Storage

- SSD holds the Proxmox OS and guest disks.
- The two 8 TB HDDs hold the media library and downloads. They are mounted into the media-server LXC at `/mnt/storage` (library, `/mnt/storage/media`) and `/mnt/downloads`.
