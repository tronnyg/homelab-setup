# Game servers (VM `pelican-panel`)

Ubuntu VM (4 vCPU, ~16 GB RAM, 200 GB disk) hosting game servers with [Pelican Panel](https://pelican.dev). The panel and its Wings daemon run on the same VM. It replaced a Pterodactyl setup.

Installed using the official install guides from the Pelican project (not Compose), so there are no config files in this repo.

## Servers

- About 10 Minecraft servers, modded and vanilla. Usually only two run at once, depending on who is playing.
- Terraria

Servers are started and stopped from the panel as needed, which keeps RAM use manageable.
