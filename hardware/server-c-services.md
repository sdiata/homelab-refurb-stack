# 🏠 Server C - Home Services Hardware

## Overview

**Role**: Home automation, surveillance, network services  
**Status**: ✅ Hardware acquired, ready for deployment  
**Power Consumption**: ~25W idle, ~35W under load

## Hardware Specifications

### Base System
- **Machine**: Lenovo ThinkCentre M720q Tiny (refurbished)
- **Status**: ✅ Acquired for €125 (eBay)
- **Form Factor**: Ultra-compact (1L volume)
- **Dimensions**: 179 × 183 × 34.5 mm
- **Mounting**: VESA mount compatible

### Compute
- **CPU**: Intel i5-8500T (6 cores, 6 threads)
  - **Base Clock**: 2.1 GHz
  - **Boost Clock**: 3.5 GHz
  - **TDP**: 35W (T-series low power)
  - **Architecture**: Coffee Lake (14nm)
  - **Features**: Perfect balance of performance and efficiency

- **CPU Upgrade Option**: Intel i7-8700T
  - **Cores/Threads**: 6c/12t (hyperthreading advantage)
  - **TDP**: 35W (same power envelope)
  - **Benefits**: Better multitasking for multiple VMs
  - **Cost**: ~€80-120 second-hand market

### Memory
- **Capacity**: 64GB SODIMM DDR4 (2×32GB)
- **Status**: 🟡 Negotiating Leboncoin deal (€129)
- **Configuration**: Dual channel
- **Speed**: DDR4-2666 (M720q supported maximum)
- **Benefit**: Generous allocation for multiple service VMs

### Storage
- **Drive**: 1× 1TB Crucial T500 NVMe Gen4
- **Status**: ✅ Acquired for €78 (Amazon)
- **Interface**: M.2 2280 PCIe Gen4
- **Performance**: Up to 7,400 MB/s read speeds
- **Purpose**: Proxmox hypervisor + all service VMs

### Network & Expansion
- **Primary Network**: 2.5GbE PCIe card + Riser
- **Status**: ✅ Acquired for €40
- **Native Network**: 1GbE (built-in, backup)
- **Expansion**: Custom riser card for low-profile PCIe

### Form Factor Benefits
- **Ultra-compact**: Fits anywhere in home
- **Silent operation**: Designed for office environment
- **Low power**: 35W maximum with T-series CPU
- **Reliable**: Enterprise-grade components
- **Serviceable**: Easy access to components

## Planned VM Configuration

### Proxmox VE Layout
```
💾 Storage Pool: T500 1TB NVMe
├── 📁 Proxmox VE OS (~15GB)
├── 🏠 VM: Home Assistant (~60-80GB)
│   └── 🔌 Smart home automation & IoT management
├── 📷 VM: DSM Surveillance (~30-50GB)  
│   └── 🎥 Doorbell & security camera management
├── 💻 VM: Development Environment (~100GB)
│   └── 🔧 Testing & development projects
└── 📦 Containers: Lightweight services
    ├── 🌩️ LXC: Cloudflared tunnel (~2GB)
    ├── 🔗 LXC: Netbird VPN mesh (~5GB)
    ├── 📡 LXC: Zigbee2MQTT bridge (~5GB) [Optional if not on RPi]
    ├── 📊 LXC: Monitoring agents (~2GB)
    └── ⚙️ System configs & logs (~30GB)
```

### VM Resource Allocation
| VM/Service | CPU Cores | RAM | Storage | Purpose |
|------------|-----------|-----|---------|----------|
| Proxmox Host | - | 8GB | 15GB | Hypervisor |
| Home Assistant | 2 | 16GB | 80GB | Smart home hub |
| DSM Surveillance | 2 | 16GB | 50GB | Camera management |
| Development | 2 | 16GB | 100GB | Testing environment |
| LXC Services | 1 | 8GB | 50GB | Network services |
| **Total** | **6c** | **64GB** | **295GB** | |
| **Remaining** | **0c** | **0GB** | **~700GB** | Future expansion |

## Service Architecture

### Home Automation Stack
- **Home Assistant OS**: Core automation platform
- **MQTT Broker**: IoT device communication
- **Node-RED**: Visual automation flows (if needed)
- **ESPHome**: Custom ESP32/ESP8266 integration

### Network Services
- **Cloudflared**: Secure tunnel for external access
- **Netbird**: Mesh VPN for remote connectivity
- **DNS**: Secondary PiHole instance (if needed)
- **VPN**: Wireguard server (via Netbird)

### Surveillance & Security
- **DSM VM**: Synology experience for camera management
- **Motion detection**: AI-powered alerts
- **Storage**: Recordings stored on Server A dataset
- **Mobile access**: Secure remote viewing

### Development Environment
- **Docker**: Container testing
- **Git repositories**: Local development
- **Database testing**: PostgreSQL/MySQL instances
- **Web services**: Nginx/Apache testing

## Network Integration

### VLAN Configuration
- **Management**: Proxmox + SSH access
- **IoT**: Isolated VLAN for smart devices
- **Surveillance**: Camera network isolation  
- **Services**: Internal service communication

### Connectivity
- **2.5GbE**: Primary connection to lab network
- **1GbE**: Backup connection (built-in)
- **WiFi**: Not used (wired preferred for reliability)

## Performance Characteristics

### Expected Performance
- **VM Boot**: Fast with NVMe storage
- **Concurrent VMs**: 3-4 simultaneously without issues
- **Network**: Wire-speed 2.5Gbps capability
- **Responsiveness**: Excellent for home automation

### Bottlenecks
- **CPU**: May limit CPU-intensive tasks
- **RAM**: Well-provisioned for planned workload
- **Storage**: Single NVMe (no redundancy)
- **Network**: 2.5GbE sufficient for use case

## Power & Thermal

### Power Consumption
- **Idle**: ~25W (T-series CPU efficiency)
- **Typical Load**: ~30W (multiple VMs)
- **Maximum**: ~35W (full CPU utilization)
- **Annual**: ~260kWh (@30W average)

### Thermal Management
- **CPU Cooling**: OEM low-profile cooler
- **Case Ventilation**: Optimized for low noise
- **Ambient**: Standard home environment
- **Monitoring**: Temperature alerts via Proxmox

## Why This Configuration?

### Form Factor: M720q Tiny
**Perfect for home lab:**
- **Compact**: Doesn't dominate living space
- **Quiet**: WAF (Wife Acceptance Factor) compliant
- **Efficient**: Low power consumption
- **Reliable**: Enterprise build quality

### CPU: i5-8500T
**Optimal balance:**
- **Performance**: 6 cores handle multiple VMs
- **Efficiency**: 35W TDP keeps power/heat low
- **Headroom**: Upgrade to i7-8700T possible

### Memory: 64GB
**Future-proof allocation:**
- **Home Assistant**: Generous for growth
- **Multiple VMs**: No memory pressure
- **Container Services**: Room for expansion
- **ZFS**: If used for datasets

### Storage: Single T500 1TB
**Performance over redundancy:**
- **Speed**: NVMe Gen4 for responsive VMs
- **Capacity**: Adequate for services
- **Backup**: VM configs replicated to Server D
- **Philosophy**: Speed for services, reliability from backups

## Upgrade Paths

### CPU Upgrade
- **Target**: Intel i7-8700T (6c/12t)
- **Benefit**: Hyperthreading for better VM density
- **Cost**: €80-120
- **Timeline**: When CPU becomes bottleneck

### Storage Expansion
- **Option 1**: Upgrade to T500 2TB NVMe
- **Option 2**: External USB storage for archives
- **Option 3**: Network storage on Server A

### Network Upgrade
- **Future**: 10GbE if lab backbone upgrades
- **Current**: 2.5GbE sufficient for foreseeable needs

## Security Considerations

### VM Isolation
- **Firewall**: Proxmox built-in firewall rules
- **VLANs**: Network segmentation
- **Access Control**: SSH key authentication
- **Updates**: Automated security patching

### External Access
- **Tunnels**: Cloudflare + Netbird (no port forwarding)
- **VPN**: Encrypted mesh connectivity
- **Monitoring**: Intrusion detection alerts
- **Backup**: Configurations backed up to Server D

## Budget Breakdown

### Acquired Components
| Component | Cost | Source | Status |
|-----------|------|---------|--------|
| M720q Tiny i5-8500T | €125 | eBay | ✅ Delivered |
| T500 1TB NVMe | €78 | Amazon | ✅ Delivered |
| 2.5GbE Card + Riser | €40 | - | ✅ Delivered |

### Pending Purchase
| Component | Cost | Source | Status |
|-----------|------|---------|--------|
| 64GB SODIMM DDR4 | €129 | Leboncoin | 🟡 Negotiating |

### Total Cost
**Current Total**: €372 (with RAM deal)

### Future Upgrades
| Upgrade | Cost | Priority |
|---------|------|----------|
| i7-8700T CPU | €80-120 | Low |
| Additional storage | €100+ | Low |

## Deployment Strategy

### Phase 1: Core Services
1. **Proxmox installation**: Base hypervisor
2. **Home Assistant VM**: Core automation
3. **Network services**: Cloudflared, Netbird

### Phase 2: Surveillance  
1. **DSM VM**: Camera management
2. **Integration**: Server A dataset for recordings
3. **Mobile access**: Secure remote viewing

### Phase 3: Development
1. **Dev VM**: Testing environment
2. **CI/CD**: Local development pipeline
3. **Monitoring**: Integration with Server D

## Monitoring & Management

### Health Monitoring
- **Hardware**: CPU, RAM, storage, temperature
- **Services**: VM status, container health
- **Network**: Connectivity and throughput
- **Integration**: Metrics sent to Server D

### Management Access
- **Local**: Direct access via monitor/keyboard (emergency)
- **Network**: SSH and web console access
- **VPN**: Secure remote management via Netbird
- **Mobile**: Proxmox mobile app for basic monitoring

## Use Cases

### Daily Operations
- **Smart Home**: Lights, heating, security automation
- **Surveillance**: Doorbell and camera monitoring  
- **Development**: Code testing and deployment
- **Network**: VPN access and secure tunneling

### Integration with Lab
- **Storage**: VM backups to Server A/D
- **Monitoring**: Health metrics to Server D
- **Networking**: Part of lab 2.5GbE backbone
- **Services**: Complementary to other servers

---

*Server C provides the essential services that make the house truly "smart" and connected, while maintaining the compact and efficient philosophy of the entire lab.* 🏠✨
