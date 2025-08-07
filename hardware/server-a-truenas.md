# 🗄️ Server A - TrueNAS Hub Hardware

## Overview

**Role**: Centralized storage, backup hub, file sharing  
**Status**: ✅ Production since December 2024  
**Power Consumption**: ~30W idle, ~50W under load

## Hardware Specifications

### Base System
- **Form Factor**: Mini-ITX build
- **Chassis**: Fractal Node 304 (compact 6-bay NAS case)
- **Power Supply**: 80+ efficient, ~200W capacity

### Compute
- **CPU**: Intel N100 (4 cores, 4 threads)
  - **Base Clock**: 1.0 GHz
  - **Boost Clock**: 3.4 GHz
  - **TDP**: 6W (ultra low power)
  - **Architecture**: Alder Lake-N (10nm)
  - **Features**: Hardware transcoding, AES-NI

### Memory
- **Capacity**: 32GB DDR4
- **Configuration**: Dual channel for optimal performance
- **Speed**: DDR4-3200 (or maximum supported)
- **ECC**: Non-ECC (sufficient for home use)

### Storage Architecture

#### Boot Pool (ZFS Mirror)
- **Drives**: 2× 250GB NVMe SSD
- **Configuration**: ZFS mirror for redundancy
- **Purpose**: TrueNAS OS, system datasets
- **Performance**: Ultra-fast boot and system responsiveness

#### Fast Pool (ZFS Mirror) 
- **Drives**: 2× 1TB NVMe SSD
- **Configuration**: ZFS mirror
- **Purpose**: High-performance datasets, VM storage
- **Use Cases**: Database storage, active projects

#### Main Storage Pool (RAID-Z1)
- **Drives**: 3× 12TB HDD (7200 RPM preferred)
- **Configuration**: RAID-Z1 (single parity)
- **Usable Capacity**: ~24TB
- **Purpose**: Bulk storage, media files, backups
- **Recommended**: WD Red Pro, Seagate IronWolf Pro

#### L2ARC Cache
- **Drive**: 1× 250GB SSD (dedicated)
- **Purpose**: Read cache for frequently accessed data
- **Target**: Immich photo dataset acceleration
- **Note**: Activated after Server B deployment

### Network
- **Primary**: 2.5GbE ethernet
- **Backup**: 1GbE ethernet (if available)
- **Purpose**: High-speed data transfers to/from lab servers

### Expansion Capabilities
- **SATA Ports**: 6+ (for HDD expansion)
- **M.2 Slots**: 2 (currently used for boot pool)
- **Fast Pool Upgrade**: Can increase NVMe capacity instead of adding drives
- **PCIe Slots**: 1× for additional networking or storage controllers
- **USB**: Multiple USB 3.0+ ports for external backup drives

## Performance Characteristics

### Expected Performance
- **Sequential Read**: 100+ MB/s (HDD pool)
- **Sequential Write**: 80+ MB/s (HDD pool)
- **Random IOPS**: Excellent (NVMe pools)
- **Network Throughput**: 2.5Gbps wire speed

### ZFS Benefits
- **Data Integrity**: Built-in checksumming and error correction
- **Snapshots**: Point-in-time recovery
- **Compression**: Available but not currently implemented
- **Replication**: Efficient backup to Server D

## Power & Thermal

### Power Consumption
- **Idle**: ~30W (N100 + drives spun down)
- **Load**: ~50W (during heavy I/O operations)
- **Annual**: ~260kWh (@30W average)

### Cooling
- **CPU**: Noctua low-profile cooler (6W TDP)
- **Case**: Fractal Node 304 optimized airflow
- **Noise**: Ultra-quiet operation

## Why This Configuration?

### CPU Choice: Intel N100
**Pros:**
- Ultra-low power consumption (6W TDP)
- Hardware transcoding capabilities
- Modern architecture with good performance
- Perfect for NAS workloads

**Sufficient for:**
- File serving and sharing
- ZFS operations
- Light transcoding
- Multiple simultaneous users

### Storage Strategy
**Boot Mirror**: Reliability for OS
**Fast Pool**: Performance for active data
**Main Pool**: Capacity for bulk storage
**L2ARC**: Acceleration for hot data

### Memory Sizing
**32GB**: Generous for ZFS caching
- ZFS ARC utilizes available RAM
- Better performance with more cache
- Sufficient for deduplication if needed

## Connectivity

### Internal Storage
```
├── Boot Pool (ZFS Mirror)
│   ├── 250GB NVMe SSD #1 (M.2 slot 1)
│   └── 250GB NVMe SSD #2 (M.2 slot 2)
├── Fast Pool (ZFS Mirror)  
│   ├── 1TB NVMe SSD #1 (PCIe card or M.2)
│   └── 1TB NVMe SSD #2 (PCIe card or M.2)
├── Storage Pool (RAID-Z1)
│   ├── 12TB HDD #1 (SATA)
│   ├── 12TB HDD #2 (SATA)
│   └── 12TB HDD #3 (SATA)
└── L2ARC Cache
    └── 250GB SSD (SATA)
```

### External Connections
- **Network**: 2.5GbE to lab switch
- **Management**: IPMI or similar (if available)
- **USB**: Backup drives, UPS monitoring

## Upgrade Path

### Immediate Expansions
- **Storage**: Add more 12TB drives to pool
- **Cache**: Upgrade L2ARC to larger/faster SSD
- **Network**: 10GbE upgrade if needed

### Long-term Options
- **Fast Pool**: Upgrade to larger NVMe drives (2TB+)
- **Storage**: Migrate to larger drives (18TB+)
- **Major Upgrade**: Motherboard replacement required for CPU/memory expansion

## Maintenance Notes

### Regular Tasks
- **Scrub**: Monthly ZFS scrub for data integrity
- **Snapshots**: Automated daily/weekly snapshots
- **Monitoring**: Drive health via SMART
- **Updates**: Regular TrueNAS updates

### Backup Strategy
- **Local**: Snapshots on same system
- **Remote**: Replication to Server D
- **Offline**: External USB drives

## Cost Breakdown

*Costs will vary based on market conditions and deals found*

| Component | Estimated Cost | Notes |
|-----------|----------------|-------|
| Mini-ITX Motherboard N100 | €170 | N100 system |
| Memory 32GB | €80-120 | DDR4 kit |
| Boot NVMe (2×250GB) | €40 | Quality brand |
| Fast NVMe (2×1TB) | €150 | Gen4 preferred |
| Storage HDDs (3×12TB) | €450 | Refurbished enterprise grade |
| L2ARC SSD (250GB) | €40-60 | SATA SSD |
| Case & PSU | €100 | Fractal Node 304 + PSU |
| **Total** | **€1030-1140** | Actual build cost |

## Services Running

### Core TrueNAS Services
- **SMB/CIFS**: Windows file sharing
- **NFS**: Unix file sharing  
- **iSCSI**: Block storage (if needed)
- **S3**: Object storage API

### Additional Applications
- **Filebrowser**: Web-based file manager
- **PiHole**: DNS ad-blocking (backup instance)
- **Cloudflare Tunnel**: Secure remote access
- **Monitoring Agent**: Metrics collection for Server D

## Network Configuration

### IP Configuration
- **Static IP**: Assigned from lab subnet
- **Hostname**: truenas-hub or similar
- **DNS**: Local DNS server (primary or backup)

### Firewall Rules
- **SMB/NFS**: Internal network only
- **Web UI**: Management subnet access
- **Replication**: Server D access only
- **External**: Via Cloudflare tunnel only

---

*Server A provides the foundation for the entire homelab - reliable, efficient, and scalable storage.*
