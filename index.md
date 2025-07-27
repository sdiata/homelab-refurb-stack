---
title: Home Lab — Low Power, Full SSD Backup, Refurb ThinkCentre Architecture
layout: default
---
# Home Lab Project 🧪

A self-hosted home infrastructure built on energy-efficient, refurbished Lenovo ThinkCentre machines using Kingston SSDs and RAM.

## 🔧 Hardware Overview

### NAS A — Main Storage
- Fractal Design Node 304
- Intel N100, 32GB RAM
- OS: TrueNAS Scale
- Boot:
  - 2× 250GB (mirror) 
- Storage:
  - 3× 12TB HDD (RAID-Z1)
  - 2× 1TB SSD (mirror)
  - 2× 1TB NVMe (mirror)

### NAS B — Full SSD Cold Replication
- Lenovo M720s SFF
- Intel® Core™ i5-9400, 32GB RAM
- OS: TrueNAS Scale
- Boot: NVMe 250GB
- 4× 2TB SSD(RAID-Z1)

### NAS C — Proxmox + Services
- Lenovo M720q Tiny
- i5-8500T, 64GB RAM
- OS: Proxmox
- Boot: 1TB (VMs)
- 1× SSD 2TB (Data)

## 📈 Goals

- Minimal energy consumption
- Zero-rack form factor
- SSD-based cold replication (ZFS)
- Open-source stack: TrueNAS, Proxmox, Home Assistant, etc.

## 📸 Coming soon

- Architecture diagrams
- Cabling plan & VLAN setup
- Build photos and performance benchmarks

---

Made with ❤️ by mamba_networks

