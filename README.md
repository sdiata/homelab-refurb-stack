# 🏠 Home Lab — Low-Power, Full-Featured NAS & Services Architecture

This project documents a complete, personal home lab infrastructure based on compact, energy-efficient refurbished Lenovo ThinkCentre mini-PCs.

> The goal: demonstrate that a full-featured, scalable homelab can be built using second-hand hardware, without noisy racks or new equipment — and still be reliable, efficient, and modern.

## 🔧 Hardware Architecture

### Server A — Main Storage & Services (OPERATIONAL)
- **CPU**: Intel N100 (quad-core)
- **RAM**: 32 GB DDR4
- **OS**: TrueNAS Scale
- **Storage**:
  - Boot pool: 2× 500GB NVMe (ZFS mirror)
  - App pool: 2× 1TB SSD SATA (ZFS mirror)
  - Critical data: 2× 2TB NVMe (ZFS mirror)
  - Media/Backups: 3× 12TB HDD (RAID-Z1)
- **Network**: 2.5 GbE native
- **Role**: Primary storage, Jellyfin, Time Machine, Nextcloud, etc.

### Server B — Cold Backup (All SSD)
- **Model**: Lenovo ThinkCentre M720s SFF
- **CPU**: Intel i5-9500 (planned: i5-8500T or i7-8700T /low power)
- **RAM**: 64 GB DDR4 DIMM (2666 MHz)
- **OS**: TrueNAS Scale (bare metal)
- **Storage**:
  - Boot: 500GB NVMe
  - Replication pool: 4× 2TB SSD SATA (RAID-Z1)
- **Network**: Realtek RTL8125B 2.5 GbE PCIe x1
- **Role**: Cold replication of critical datasets from NAS A

### Server C — Services & Virtualization (Proxmox VE)
- **Model**: Lenovo ThinkCentre M720q Tiny
- **CPU**: Intel i5-8500T (planned: i7-8700T or i9-9900T /low power)
- **RAM**: 128 GB DDR4 SODIMM (2666 MHz)
- **Storage**:
  - VM disk: 1 TB NVMe
  - VM data/backup: 2 TB SSD SATA
- **Network**: 2.5 GbE native
- **Role**: Lightweight VMs (Home Assistant, Node-RED, MQTT, Immich, Grafana etc.) + Ollama (LLMs)

## 🚀 Planned Services & Applications

### **Server A — Core Services**
* **Media Stack**: Jellyfin (4K streaming), Sonarr, Radarr, Prowlarr
* **File Sync**: Nextcloud (self-hosted cloud storage)
* **Backup**: Time Machine targets for macOS clients

### **Server C — Virtualized Services**
* **Home Automation**: Home Assistant + Node-RED (50+ IoT devices)
* **Photo Management**: Immich (AI-powered Google Photos alternative)
* **Surveillance**: Frigate NVR + Coral TPU (AI object detection)
* **AI/ML**: Ollama (local LLM inference), Whisper (speech-to-text)
* **Monitoring**: Grafana, InfluxDB, Prometheus, Node Exporter
* **Remote Access**: Cloudflare Tunnel (secure external access)
* **Network**: Pi-hole (DNS filtering), Unbound (recursive DNS)

### **Infrastructure Services**
* **Storage**: ZFS replication (A → B), automated snapshots
* **Network**: VLAN segmentation (IoT/Services/Management/Storage)
* **Security**: Zero Trust access, SSL termination, DDoS protection

## 📈 Build Progress
- [x] Server A operational (Intel N100 + 32GB) (OPERATIONAL)
- [ ] Server B completion (awaiting DDR4 & SSD components)
- [ ] Server C deployment (awaiting NVMe & 128GB DDR4)
- [ ] Full stack integration & testing

## 🎯 Project Goals

- 💡 Minimal power usage (< 30W per node)
- 🧩 Scalable design (RAID-Z, VMs, VLANs)
- 🔐 Data safety via ZFS replication
- ♻️ Full use of refurbished & recycled hardware
- 🌐 Open-source stack (Proxmox, TrueNAS, HA, Immich...)
- 📚 Complete documentation for community replication
- 🎥 Video tutorials and build guides
- 🔬 Long-term reliability validation (6+ months uptime)

## 🧪 Next Steps

- Network topology with VLANs & firewall rules
- Storage benchmarks & power consumption metrics
- Service migration and CI/CD for HA deployments

## 🌟 Community Impact
- GitHub documentation for replication
- YouTube build series (planned Q4 2025)
- Collaboration with homelab creators
- French + English tutorials for broader reach
---

Maintained by @sdiata(https://github.com/sdiata) · All feedback welcome!

