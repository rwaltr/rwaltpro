---
title: "My Local Setup"
showDate: false
showWordCount: false
SharingLinks: false
showPagination: false
showAuthor: false
showHero: false
showTableOfContents: true
---

The laptop I actually work on, and the reasoning behind how it's set up. It's deliberately terminal-first and reproducible - if this machine died, a new one would look like it within the hour.

## The setup

| Layer | What |
| --- | --- |
| Hardware | [Framework Laptop 13](https://frame.work/) - AMD Ryzen 5 7640U, 30GB RAM, 2TB WD_BLACK SN770 (LUKS), Radeon 760M |
| OS | [Zirconium](https://github.com/zirconium-dev/zirconium) 44 - an opinionated Fedora bootc image (immutable, image-based updates) running the Niri compositor |
| Terminal | [foot](https://codeberg.org/dnkl/foot) + [fish](https://fishshell.com/) + [zellij](https://zellij.dev/) |
| Shell niceties | [starship](https://starship.rs/), [atuin](https://atuin.sh/), [zoxide](https://github.com/ajeetdsouza/zoxide) |
| Editor | [Neovim](https://neovim.io/) on LazyVim |
| Keyboard | [MoErgo Go60](https://moergo.com/) - split ergonomic |
| Phone | Pixel running [GrapheneOS](https://grapheneos.org/) |
| CLI toolkit | ripgrep, fd, fzf, bat, eza, yazi, television, jq, yq, delta, gitui, bottom, dust, hyperfine |
| Containers | Rootless [Podman](https://podman.io/) + [Distrobox](https://distrobox.it/) |
| Tooling | [mise](https://mise.jdx.dev/) for tools and tasks, [chezmoi](https://www.chezmoi.io/) for dotfiles, [Tailscale](https://tailscale.com/) for access, kubectl + [k9s](https://k9scli.io/), [restic](https://restic.net/) + rclone for backups |
| Secrets | 1Password CLI via [fnox](https://fnox.jdx.dev/) |

## Why these choices

| Decision | Reasoning |
| --- | --- |
| Image-based OS | Zirconium updates by swapping images, so the laptop stays reproducible and rolling back is free. |
| Terminal-first | foot is Wayland-native and fast; fish plus zellij makes long-lived sessions and SSH into the cluster pleasant. |
| Neovim on LazyVim | Keyboard-driven, behaves identically over SSH and locally, and its config is just files in chezmoi. |
| Rootless containers | Podman with no daemon and no root; Distrobox when a task wants another distro's toolchain. |
| mise + chezmoi | Tools and configuration are declared, so any machine becomes *my* machine in minutes. |
| Tailscale | Private access to the homelab from anywhere without opening a port. |
| Split keyboard | Ergonomic and built to last - the biggest day-to-day quality-of-life upgrade I've made. |
| GrapheneOS | Hardened Android with no Google services by default. |
