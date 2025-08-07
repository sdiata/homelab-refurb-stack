# 🤖 Server B - AI & Creative Hardware

⚠️ **UNDER CONSTRUCTION** - Hardware sourcing in progress

## Overview

**Role**: Artificial intelligence, multimedia processing, creative workstation  
**Status**: 🔄 Hardware acquisition phase  
**Target Power**: ~50W idle, ~150W under full GPU load (Phase 3)

## Current Sourcing Challenges

### 🔍 Active Search Items
- **64GB DDR4 DIMM**: Struggling to find affordable options (~€100-120 target)
- **2× KC600 1TB SSD**: Looking for equivalent enterprise SSD alternatives
- **RTX A2000**: Phase 3 GPU - monitoring second-hand market

*If you have leads on affordable enterprise hardware in EU, contributions welcome!*

## Hardware Specifications

### Base System
- **Machine**: Lenovo ThinkCentre M720s SFF (refurbished)
- **Status**: ✅ Acquired for €90 (eBay)
- **Form Factor**: Small form factor (SFF)
- **Expansion**: PCIe x16 slot for GPU (Phase 3)

### Compute
- **CPU**: Intel i5-9400 (6 cores, 6 threads)
  - **Base Clock**: 2.9 GHz
  - **Boost Clock**: 4.1 GHz
  - **TDP**: 65W
  - **Architecture**: Coffee Lake (14nm)
  - **Features**: Good multi-core performance for AI workloads
- **CPU Upgrade Path**: i7-8700T (35W TDP) or i9-9900T (35W TDP)
  - **i7-8700T**: 6c/12t, hyperthreading advantage for AI
  - **i9-9900T**: 8c/16t, maximum performance in low-power envelope
  - **Benefit**: Better multithreading + lower power consumption

### Memory
- **Target**: 64GB DDR4 DIMM (2×32GB)
- **Status**: 🔄 **Searching for affordable options**
- **Budget Target**: €100-120 (struggling to find at this price)
- **Speed**: DDR4-2666 minimum (M720s supported)
- **Upgrade Path**: 128GB in Phase 3 for heavy AI workloads

### Storage Architecture

#### Boot Pool (SSD Mirror)
- **Drives**: 2× 250GB Crucial BX SSD
- **Status**: ✅ Recovered from previous build
- **Configuration**: ZFS mirror for redundancy
- **Purpose**: Proxmox VE hypervisor

#### VM Storage (Enterprise SSD)
- **Drive**: 1× 1TB KC600 SSD  
- **Status**: ✅ Found on eBay (€77)
- **Configuration**: Single drive (no mirror initially)
- **Future**: Can add second drive later if needed
- **Purpose**: Proxmox VMs, Ollama models, development

#### High-Performance Storage
- **Drive**: 1× 2TB Crucial T500 NVMe Gen4
- **Status**: 🔄 Considering upgrade from 1TB to 2TB
- **Configuration**: Single drive (performance focus)
- **Purpose**: 
  - Immich photo storage and processing
  - ZIL/SLOG partition (~150GB)
  - Working cache for creative applications

### Network & Expansion
- **Primary**: 2.5GbE PCIe card
- **Status**: ✅ Acquired for €20
- **Additional**: PCIe x1 → 4× SATA controller
- **Status**: ✅ Acquired for €20
- **GPU Slot**: PCIe x16 available for Phase 3

### Phase Evolution

#### Phase 1 (Current) - Basic AI
- **GPU**: None (CPU-only AI processing)
- **AI Capability**: Light Ollama models, basic Immich
- **Creative**: Limited to CPU-based processing

#### Phase 2 - AI Acceleration  
- **Addition**: Coral TPU USB (~€70)
- **AI Boost**: Ultra-fast object detection for Immich
- **Power**: +2W minimal increase
- **Status**: Planned after Phase 1 completion

#### Phase 3 - Creative Powerhouse
- **GPU**: RTX A2000 
- **Status**: 🔄 **Monitoring second-hand market (~€300-400)**
- **RAM**: Additional 64GB (128GB total)
- **Capabilities**: 
  - 4K video editing (DaVinci Resolve)
  - AI image generation (Stable Diffusion)  
  - GPU-accelerated photo editing
  - Hardware transcoding

## Performance Targets

### Phase 1 Performance
- **Immich**: Good performance with CPU transcoding
- **Ollama**: 7B-13B models with reasonable speed
- **VMs**: Smooth Proxmox operation
- **Limitations**: No GPU acceleration

### Phase 3 Performance  
- **Video Editing**: 4K timeline editing
- **AI Generation**: Fast Stable Diffusion inference
- **Photo RAW**: Hardware-accelerated processing
- **Transcoding**: Multiple simultaneous streams

## Current Build Status

### ✅ Acquired Components
| Component | Cost | Source | Notes |
|-----------|------|---------|-------|
| M720s SFF Base | €90 | eBay | Good condition |
| 2.5GbE Network Card | €20 | - | PCIe x1 |
| SATA Controller | €20 | - | PCIe x1 → 4× SATA |
| Boot SSDs (2×250GB) | €0 | Recovered | Crucial BX series |

### 🔄 Searching For
| Component | Target Budget | Status | Notes |
|-----------|---------------|--------|-------|
| **64GB DDR4 DIMM** | **€100-120** | **Struggling** | 2×32GB sticks needed |
| **1× KC600 1TB** | **€77** | **Found** | eBay deal |
| T500 2TB NVMe | €140 | Considering | Upgrade from 1TB option |

### 📅 Future Phases
| Component | Target Budget | Timeline | Priority |
|-----------|---------------|----------|----------|
| CPU Upgrade (i7-8700T) | €80-120 | Phase 2 | Medium |
| CPU Upgrade (i9-9900T) | €150-200 | Alternative | Low |
| Coral TPU USB | €70 | Phase 2 | Medium |
| RTX A2000 | €300-400 | Phase 3 | High |
| Additional 64GB RAM | €100-120 | Phase 3 | High |

## Storage Layout Plan

### Proxmox VE Configuration
```
📁 Boot Pool (250GB × 2 mirror)
├── 📄 Proxmox VE OS (~10GB)
├── 📄 System configs (~5GB)  
└── 📄 Templates & ISOs (~50GB)

📁 VM Storage (1TB single drive)  
├── 🖥️ Development VMs (~200GB)
├── 🤖 Ollama LLM models (~300GB)
├── 🐳 Docker containers (~100GB)
└── 📊 Logs & monitoring (~50GB)

📁 Fast Storage (T500 2TB)
├── 📸 Immich photos & cache (~1.7TB)
├── ⚡ ZIL/SLOG partition (~150GB)  
└── 🎨 Creative project cache (~100GB)
```

## Creative Applications Stack

### Photo Processing
- **RawTherapee**: RAW development
- **GIMP**: Advanced photo editing
- **Hardware**: RTX A2000 acceleration (Phase 3)

### Video Editing  
- **DaVinci Resolve**: Professional editing suite
- **Hardware**: RTX A2000 + 128GB RAM (Phase 3)
- **Performance**: 4K timeline editing capability

### AI Applications
- **Immich**: Intelligent photo management with facial recognition
- **Ollama**: Local LLM inference for text generation
- **Stable Diffusion**: Image generation (Phase 3)
- **Creative AI Workflow**:
  - **Scriptwriting**: Ollama for story development, dialogue, scene descriptions  
  - **Storyboarding**: LLM generates shot descriptions → Stable Diffusion creates visual concepts
  - **Pre-visualization**: AI-generated mockups before actual filming/editing

## Network Integration

### Lab Connectivity
- **2.5GbE**: High-speed connection to Server A (TrueNAS)
- **Photo Workflow**: Camera → Immich → TrueNAS dataset
- **L2ARC**: Server A provides read cache for photos
- **Backup**: VM configs replicated to Server D

### Remote Access
- **VNC/RDP**: Creative applications from Mac
- **SSH**: Command line management  
- **Netbird**: Mesh VPN for secure remote access
- **Cloudflare**: Backup secure tunnel access

## Power & Thermal Considerations

### Power Consumption by Phase
- **Phase 1**: ~50W (i5-9400 + drives)
- **Phase 1 + CPU upgrade**: ~35W (i7-8700T/i9-9900T + drives)
- **Phase 2**: ~37W (+TPU, post CPU upgrade)  
- **Phase 3**: ~120W (low-power CPU + RTX A2000)

### Thermal Management
- **SFF Form**: Adequate cooling for CPU
- **GPU**: RTX A2000 low-profile, efficient
- **Ambient**: Standard office environment suitable

## Compatibility Notes

### M720s SFF Limitations
- **RAM**: Maximum officially supported varies
- **GPU**: Low-profile cards required
- **Power**: 180W PSU limits GPU choices
- **Cooling**: Compact case affects thermals

### Verified Compatible
- **RTX A2000**: Confirmed fit and power requirements
- **64GB DDR4**: Should work (seeking confirmation)
- **Multiple PCIe cards**: Tested configuration

## Budget Summary

### Phase 1 Target
| Phase | Current Cost | Missing | Total Target |
|-------|--------------|---------|--------------|
| **Phase 1** | €130 | €390-450 | **€520-580** |

### Full Build Cost  
| Phase | Incremental | Cumulative |
|-------|-------------|------------|
| Phase 1 | €520-580 | €520-580 |
| Phase 2 | +€70 | €590-650 |  
| Phase 3 | +€400-520 | **€990-1170** |

## Community Help Wanted

### If You Have Leads On:
- **Affordable 64GB DDR4**: EU suppliers or deals
- **Enterprise SATA SSDs**: KC600 alternatives  
- **RTX A2000 deals**: Second-hand market tips
- **M720s experience**: Compatibility confirmations

**Contributing**: Open issues or discussions with hardware tips!

## Why This Configuration?

### CPU: Intel i5-9400
- **Good value**: Solid 6-core performance
- **AI suitable**: Decent for CPU-based inference
- **Upgradeable**: GPU addition transforms capabilities

### Memory: 64GB → 128GB
- **AI hungry**: Large language models need RAM
- **Creative**: 4K video editing benefits from memory
- **Future-proof**: Capacity for growing AI models

### Storage Strategy
- **Boot reliability**: Mirror for system stability
- **VM performance**: Enterprise SSDs for databases/containers  
- **Speed where needed**: NVMe for active creative work

---

*Server B will be the creative and AI powerhouse of the lab - when the hardware hunt succeeds!* 🎯

## Status Updates

**Last Updated**: [Current Date]  
**Next Milestone**: Secure 64GB DDR4 and enterprise SSDs

**Progress**: 
- ✅ Base system acquired
- ✅ Network and expansion cards  
- 🔄 Memory and storage sourcing
- ⏳ Waiting for good deals
