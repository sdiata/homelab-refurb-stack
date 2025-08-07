# 🏠 4-Server Homelab - Compact & Eco-Friendly Self-Hosting

> **Professional architecture at affordable price - Budget ~€1100-1200**  
> *Refurbish first, No e-waste, Low power, Accessible to all*

## 🎯 Project Philosophy

This homelab demonstrates that it's possible to create a complete personal infrastructure without breaking the bank or polluting the environment. By prioritizing refurbished hardware and a progressive approach, we achieve professional performance at homelab budget.

**Core values:**
- ♻️ **Eco-friendly**: Reuse enterprise hardware
- ⚡ **Low-power**: Controlled consumption (~150W total)
- 💰 **Accessible**: Realistic budget for everyone
- 📈 **Scalable**: Progressive scaling
- 🔒 **Sovereign**: Exit Google Drive, iCloud & co

## 🏗️ Architecture Overview

### System Overview

**Simple Architecture:**

```
Internet
    ↕
[Router 2.5GbE]
    ↕
┌───────────────────────────────────────┐
│            LOCAL NETWORK              │
│                                       │
│  [A] ←→ [B] ←→ [C] ←→ [D]            │
│   │      │      │      │              │
│ TrueNAS  AI   Services Backup         │
│ 36TB   Photos Smart Home Archives     │
└───────────────────────────────────────┘
```

**Main flows:**
- **Photo upload**: Smartphone → B (Immich) → A (storage)
- **Daily backup**: A → D (replication)  
- **Remote access**: Internet → Cloudflare → Lab
- **Control**: Mac → VNC/SSH → Servers

###🌐 Network Architecture

**Physical Layer**

- Switch: Managed 2.5GbE (4+ ports)
- Connections: A, B, C → 2.5GbE | D → 1GbE
- Uplink: ISP router/modem

**Logical Layer**

- Management VLAN: Server admin access
- IoT VLAN: Smart home devices (isolated)
- Services VLAN: Internal lab communication
- Guest VLAN: Visitor network isolation

**External Access**

- Primary: Netbird mesh VPN
- Backup: Cloudflare tunnels
Philosophy: Zero port forwarding##


##🖥️ Server Details

### 🗄️ Server A - TrueNAS Hub
**Role**: Centralized storage, backup, file sharing
- **Status**: ✅ Already built (December 2024)
- **CPU**: Intel N100 (4c/4t, 6W)
- **RAM**: 32GB DDR4
- **Storage**:
  - Boot: 2×250GB NVMe mirror
  - Fast Pool: 2×1TB NVMe mirror
  - Storage: 3×12TB HDD RAID-Z1 (24TB net)
  - L2ARC: 250GB SSD dedicated (Immich photos)
- **Services**: TrueNAS Scale, Filebrowser, SMB/NFS, PiHole (backup)

### 🤖 Server B - AI & Creative
**Role**: Artificial intelligence, multimedia processing
- **Machine**: Lenovo M720s SFF (refurbished)
- **CPU**: Intel i5-9400 (6c/6t)
- **RAM**: 64GB DDR4 (→128GB Phase 3)
- **Storage**:
  - Boot: 2×250GB SSD mirror (Crucial BX reused)
  - VMs: 2×1TB KC600 mirror (Proxmox + Ollama)
  - Immich: 2TB T500 NVMe Gen4 (+ ZIL/SLOG partition)
- **GPU**: RTX A2000 (Phase 3)
- **Services**: Proxmox, Immich, Ollama, DaVinci Resolve, GIMP

### 🏠 Server C - Home Services  
**Role**: Home automation, surveillance, network services
- **Machine**: Lenovo M720q Tiny (refurbished)
- **CPU**: Intel i5-8500T (6c/6t, 35W)
- **RAM**: 64GB SODIMM DDR4
- **Storage**: 1TB T500 NVMe Gen4
- **Services**: 
  - Proxmox hypervisor
  - Home Assistant (smart home)
  - DSM VM (doorbell surveillance)
  - Zigbee2MQTT, Cloudflared, Netbird VPN

### 💾 Server D - Replication & Archive
**Role**: Backup, replication, cold storage
- **Machine**: HP EliteDesk 800 G4 SFF (refurbished)
- **CPU**: Intel i5-8500 (6c/6t, 65W)
- **RAM**: 16GB DDR4 (existing)
- **Storage**:
  - Boot: 2×250GB NVMe WD mirror
  - Archive: 2×4TB HDD (Synology recovery)
  - Fast: 2×1TB SSD mirror (Server A recovery)
  - Offline: 6TB USB external (air-gap backup)
- **Services**: TrueNAS Scale, daily replication, centralized monitoring

## 💰 Indicative Budget

**Total lab cost: ~€1100-1200**

| Server | Budget | Notes |
|---------|--------|-------|
| **Server A** | TrueNAS Hub in prod | Already built |
| **Server B** | ~€550-600 | AI & creative |
| **Server C** | ~€350-400 | Compact services |
| **Server D** | ~€200-250 | Backup & monitoring |

**Upgrades:**
- **+€70**: Coral TPU (Phase 2)
- **+€400**: RTX A2000 + 64GB RAM (Phase 3)

*Indicative prices FR second-hand market - Variable according to opportunities*

## 🚀 Scaling Phases

### Phase 1 - Base Infrastructure
- **Goal**: Complete functional lab
- **Services**: Storage, smart home, surveillance
- **AI**: CPU only (light Ollama)

### Phase 2 - AI Acceleration
- **Addition**: Coral TPU USB
- **Gain**: Ultra-fast object detection Immich
- **Consumption**: +2W only

### Phase 3 - Creative Power
- **Addition**: RTX A2000 + 64GB additional RAM
- **Capabilities**: 4K editing, generative AI, GPU rendering
- **Usage**: Complete creative studio controlled from Mac

## 🌟 Key Features

### Technical
- **Redundancy**: Mirrors on all critical components
- **Performance**: NVMe Gen4, intelligent L2ARC, 2.5GbE
- **Security**: Triple backup (A→D→USB offline)
- **Monitoring**: Complete lab supervision

### Economic
- **Fast ROI**: 2-year payback vs cloud (Drive + iCloud)
- **Scalability**: Progressive investment according to needs
- **Durability**: Enterprise hardware, easily found parts

### Environmental
- **No e-waste**: Second life for enterprise machines
- **Low power**: 35W TDP after CPU upgrades
- **Compact**: Minimal footprint vs traditional racks

## 🎯 Use Cases

### Complete Self-Hosting
- **Photos**: Immich with AI (exit Google Photos)
- **Files**: Filebrowser + Cloudflare (exit Google Drive)
- **Smart Home**: Home Assistant + Zigbee
- **Surveillance**: DSM + IP cameras

### Creativity & AI
- **Photo**: RawTherapee + GIMP (RAW workflow)
- **Video**: DaVinci Resolve (pro editing)
- **AI**: Ollama LLMs + Stable Diffusion
- **Control**: Mac interface → Lab power

## 🔧 Technical Prerequisites

### Knowledge
- **Linux**: Basic system administration
- **Docker**: Service containerization
- **Network**: VLANs, routing, DNS
- **Backup**: 3-2-1 strategies

### Tools
- **Proxmox**: Type-1 hypervisor
- **TrueNAS**: ZFS, snapshots, replication
- **Docker Compose**: Service orchestration
- **Cloudflare**: Secure tunnels

## 📚 Repository Structure

```
📁 homelab/
├── 📄 README.md (this file)
├── 📁 hardware/
│   ├── server-a-truenas.md
│   ├── server-b-ai.md
│   ├── server-c-services.md
│   └── server-d-replication.md
├── 📁 budget/
│   ├── detailed-costs.md
│   └── purchase-sources.md
├── 📁 setup/
│   ├── truenas-installation.md
│   ├── proxmox-configuration.md
│   └── docker-services.md
├── 📁 configs/
│   ├── docker-compose/
│   ├── scripts/
│   └── monitoring/
└── 📁 docs/
    ├── network-setup.md
    ├── backup-strategy.md
    └── troubleshooting.md
```

## 🤝 Contribution

This project aims to democratize self-hosting. Your feedback, improvements and adaptations are welcome!

**Philosophy**: *Accessible, documented, reproducible*

---

*"A €1000 lab that replaces €200/year of cloud, it's worth it!"* 💪

## 📞 Support & Community

- **Issues**: Technical questions, bugs, improvements
- **Discussions**: Adaptations, feedback
- **Wiki**: Community documentation

**Happy self-hosting!** 🏠✨
