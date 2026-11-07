---
title: "My Homelab Stack"
showDate: false
showWordCount: false
SharingLinks: false
showPagination: false
showAuthor: false
showHero: false
showTableOfContents: true
---

A Minisforum MS-01 with a TerraMaster 6-bay DAS under the desk, running my own domains and managed entirely from git. The whole thing lives in a single monorepo: [home-ops](https://github.com/rwaltr/home-ops).

## The stack

| Layer | Component |
| --- | --- |
| Host OS | [Flatcar Container Linux](https://www.flatcar.org/) - immutable, configured with Butane → Ignition; ZFS from the official systemd-sysext |
| Kubernetes | Single-node [k0s](https://k0sproject.io/) (v1.36) |
| CNI / load balancing | [Cilium](https://cilium.io/) as the kube-proxy replacement, with BGP for LoadBalancer IPs |
| Ingress | [Envoy Gateway](https://gateway.envoyproxy.io/) |
| GitOps | [Flux](https://fluxcd.io/) (flux-operator + flux-instance), rooted at `infra/k8s/kyz` |
| Storage | [OpenEBS](https://openebs.io/) `openebs-hostpath` on the OS NVMe; a ZFS `tank` pool (raidz1×2) on the DAS, kept outside the PVC lifecycle |
| Backups | [kopiur](https://github.com/home-operations/kopiur) + [kopia](https://kopia.io/) → RustFS (S3) on `tank/backup/k8s` |
| Secrets | 1Password Connect + External Secrets in-cluster; fnox for local and CI tooling |
| Network | MikroTik RB5009, VLAN-segmented bridge, ULA IPv6, Cloudflare + Porkbun via Terraform, Tailscale for access |
| AI | A [LiteLLM](https://www.litellm.ai/) gateway fronting [Ollama](https://ollama.com/) and [Speaches](https://github.com/speaches-ai/speaches) |
| Apps | FreshRSS, Jellyfin, Home Assistant, Mosquitto |

## Why these choices

This stack is a migration away from uCore + Quadlets, and every choice below comes from the [decision log](https://github.com/rwaltr/home-ops/blob/master/REFACTOR_PLANS.md) rather than from first principles. None of it is the "best" stack in the abstract; it's the stack that fits one person who wants to understand all of it.

| Decision | Why |
| --- | --- |
| Flatcar over uCore | A/B image updates, a smaller surface, and an official ZFS sysext (dm-verity signed, Secure Boot fine, version-locked to the release). The sysext is tagged experimental and is data-pools-only - fine here, where the OS has its own NVMe. |
| k0s via k0sctl | Better IPv6 support than the alternatives, and k0sctl is SSH-based and distro-agnostic. The documented `--profile flatcar` is stale and wedges the node - dropping the flag is the fix. |
| Cilium as CNI + kube-proxy replacement | The BGP control plane replaces MetalLB and L2 announcements, so there's no separate load balancer to run. |
| Cilium BGP for VIPs | The router speaks BGP, so service VIPs are announced as /32s from a dedicated service CIDR. |
| MikroTik over UniFi | The nerd mindset versus a simple pane of glass. UniFi wishes it were as good as MikroTik. |
| Envoy Gateway (Gateway API) | Two Gateways - internal and external - with pinned VIPs; apps attach with a single `route:` line. |
| Flux (flux-operator + flux-instance) | One root Kustomization; Kustomize components carry the cross-cutting concerns. Uniformity beats cleverness. |
| bjw-s app-template via OCIRepository | One values schema for every app, with images digest-pinned. |
| OpenEBS hostpath on the OS NVMe (non-default class) | ZFS LocalPV was rejected: its `poolname` has to match a zpool topology, and I want `tank` to stay outside the PVC lifecycle. |
| kopiur snapshots → RustFS (S3) | RustFS is the S3 backend. A Kustomize component collapsed 17 hand-written backup files into one greppable line per app. |
| Multus + macvlan, only for L2-dependent apps | Routed BGP VIPs cover everything else; L2 is only for discovery-dependent apps like Home Assistant. |
| No swap, deliberate reboots | Flatcar ships no swap, which is fine for k8s. And `REBOOT_STRATEGY=off` keeps updates staged until I choose to reboot. |
| Zero secrets in git | 1Password Connect + External Secrets in-cluster, fnox for tooling. SOPS + age was the earlier plan; it lost. |

