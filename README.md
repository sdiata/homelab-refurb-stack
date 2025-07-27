# 🏠 Home Lab — Low-Power, Full-Featured NAS & Services Architecture

This project documents a complete, personal home lab infrastructure based on compact, energy-efficient refurbished Lenovo ThinkCentre mini-PCs.

> The goal: demonstrate that a full-featured, scalable homelab can be built using second-hand hardware, without noisy racks or new equipment — and still be reliable, efficient, and modern.

## 🔧 Hardware Architecture

### NAS A — Main Storage & Services
- **CPU**: Intel N100 (quad-core)
- **RAM**: 32 GB DDR4
- **OS**: TrueNAS Scale
- **Storage**:
  - Boot pool: 2× 240 GB NVMe (ZFS mirror)
  - App pool: 2× 1 TB SSD SATA (ZFS mirror)
  - Critical data: 2× 2 TB NVMe (ZFS mirror)
  - Media/Backups: 3× 12 TB HDD (RAID-Z1)
- **Network**: 2.5 GbE native
- **Role**: Primary storage, Jellyfin, Time Machine, Nextcloud, etc.

### NAS B — Cold Backup (All SSD)
- **Model**: Lenovo ThinkCentre M720s SFF
- **CPU**: Intel i5-9500
- **RAM**: 64 GB DDR4 DIMM (2666 MHz)
- **OS**: TrueNAS Scale (bare metal)
- **Storage**:
  - Boot: 250 GB NVMe
  - Replication pool: 4× 2 TB SSD SATA (RAID-Z1)
- **Network**: Realtek RTL8125B 2.5 GbE PCIe x1
- **Role**: Cold replication of critical datasets from NAS A

### NAS C — Services & Virtualization (Proxmox VE)
- **Model**: Lenovo ThinkCentre M720q Tiny
- **CPU**: Intel i5-8500T (planned: i7-8700T or i9-9900T)
- **RAM**: 64–128 GB DDR4 SODIMM (2666 MHz)
- **Storage**:
  - VM disk: 1 TB NVMe
  - VM data/backup: 2 TB SSD SATA
- **Role**: Lightweight VMs (Home Assistant, Node-RED, MQTT, Immich, Grafana etc.)

## 🎯 Project Goals

- 💡 Minimal power usage (< 30W per node)
- 🧩 Scalable design (RAID-Z, VMs, VLANs)
- 🔐 Data safety via ZFS replication
- ♻️ Full use of refurbished & recycled hardware
- 🌐 Open-source stack (Proxmox, TrueNAS, HA, Immich...)

## 🧪 Next Steps

- Network topology with VLANs & firewall rules
- Storage benchmarks & power consumption metrics
- Service migration and CI/CD for HA deployments

---

Maintained by @sdiata(https://github.com/sdiata) · All feedback welcome!

