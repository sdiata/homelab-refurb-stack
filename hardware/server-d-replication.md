# 💾 Server D - Replication & Archive Hardware

## Overview

**Role**: Backup hub, replication target, centralized monitoring  
**Status**: ✅ Complete and operational  
**Power Consumption**: ~40W idle, ~60W during backup operations

## Hardware Specifications

### Base System
- **Machine**: HP EliteDesk 800 G4 SFF (refurbished)
- **Status**: ✅ Acquired for €144 (Backmarket)
- **Form Factor**: Small Form Factor (SFF)
- **Dimensions**: ~340 × 95 × 295 mm
- **Build Quality**: Enterprise-grade reliability

### Compute
- **CPU**: Intel i5-8500 (6 cores, 6 threads)
  - **Base Clock**: 3.0 GHz
  - **Boost Clock**: 4.1 GHz
  - **TDP**: 65W (standard power)
  - **Architecture**: Coffee Lake (14nm)
  - **Features**: Solid performance for backup and monitoring tasks

### Memory
- **Capacity**: 16GB DDR4 (2×8GB)
- **Status**: ✅ Recovered from previous build
- **Configuration**: Dual channel
- **Speed**: DDR4-2666
- **Adequacy**: Sufficient for TrueNAS and monitoring services

### Storage Architecture

#### Boot Pool (NVMe Mirror)
- **Drives**: 2×250GB NVMe (WD, different references)
- **Status**: ✅ Recovered from previous builds
- **Configuration**: ZFS mirror for OS redundancy
- **Purpose**: TrueNAS OS, system datasets
- **Note**: Asymmetric brands but same capacity (works fine)

#### Archive Storage (HDD Mirror)
- **Drives**: 2×4TB HDD (7200 RPM)
- **Status**: ✅ Recovered from Synology
- **Configuration**: ZFS mirror for maximum reliability
- **Purpose**: Long-term archive, replication target
- **Capacity**: ~4TB usable (mirrored)

#### Fast Storage (SSD Mirror)
- **Drives**: 2×1TB SSD
- **Status**: ✅ Transferred from Server A
- **Configuration**: ZFS mirror
- **Purpose**: Fast pool matching Server A fast pool
- **Use Case**: Active backup data that needs quick access

#### Offline Backup (USB External)
- **Drive**: 6TB HDD in USB enclosure
- **Status**: ✅ Available for air-gap backup
- **Purpose**: Ultimate backup layer (3-2-1 strategy)
- **Schedule**: Weekly/monthly offline backup
- **Storage**: Disconnected when not in use

### Expansion Hardware
- **SATA Controller**: PCIe x1 → 4×SATA ports
- **Status**: ✅ Acquired for €35 (includes splitter)
- **Purpose**: Connect all 4 internal drives (2×HDD + 2×SSD)
- **Additional**: SATA power splitter for drive power

#### Storage Mounting Hardware
- **Drive Screws**: Various sizes for HDD and SSD mounting
- **Status**: ✅ Acquired for €20
- **Purpose**: Proper drive mounting in SFF case
- **Includes**: 2.5" and 3.5" mounting hardware

### Network
- **Primary**: 1GbE ethernet (built-in)
- **Backup Role**: Sufficient bandwidth for replication
- **No 2.5GbE**: Cost optimization (backup doesn't need high speed)

## Storage Layout

### ZFS Pool Configuration
```
💾 Server D Storage Architecture
├── 🥾 Boot Pool (ZFS Mirror)
│   ├── 250GB NVMe WD #1 (M.2 slot 1)
│   └── 250GB NVMe WD #2 (M.2 slot 2)
├── 🗃️ Archive Pool (ZFS Mirror)
│   ├── 4TB HDD #1 (SATA via controller)
│   └── 4TB HDD #2 (SATA via controller)
├── ⚡ Fast Pool (ZFS Mirror)
│   ├── 1TB SSD #1 (SATA via controller)
│   └── 1TB SSD #2 (SATA via controller)
└── 💿 Offline Backup
    └── 6TB USB HDD (air-gap backup)
```

### Data Flow Strategy
```
📊 Backup & Replication Flow
┌─────────────┐    Daily     ┌─────────────┐
│  Server A   │─────────────►│  Server D   │
│  (TrueNAS)  │  Replication │ (Archive)   │
│   Primary   │              │   Target    │
└─────────────┘              └─────────────┘
                                     │
                                     │ Quarterly
                                     ▼
                             ┌─────────────┐
                             │   USB 6TB   │
                             │  Offline    │
                             │  Backup     │
                             └─────────────┘
```

## Services & Monitoring

### Core TrueNAS Services
- **ZFS Replication**: Receive snapshots from Server A
- **Snapshot Management**: Local snapshots for point-in-time recovery
- **Scrub Scheduling**: Monthly data integrity verification
- **SMART Monitoring**: Drive health surveillance

### Centralized Monitoring Stack
- **Prometheus**: Metrics collection server
- **Grafana**: Dashboard and visualization
- **Node Exporter**: Metrics from all lab servers (A, B, C)
- **Alert Manager**: Notification system for issues

#### Monitored Metrics
- **System Health**: CPU, RAM, disk usage, temperature
- **Network**: Bandwidth utilization, connectivity
- **Services**: Application availability, response times
- **Storage**: ZFS pool health, scrub status, drive SMART data
- **Power**: UPS status (if connected)

### Backup Verification
- **Automated Testing**: Regular restore tests
- **Integrity Checks**: Verify backup completeness
- **Alerting**: Notification of backup failures
- **Reporting**: Weekly backup status reports

## Network Integration

### Lab Connectivity
- **1GbE Connection**: Adequate for backup operations
- **Replication Schedule**: Off-peak hours (typically nights)
- **Monitoring Access**: 24/7 dashboard availability
- **Management**: SSH and web interface access

### Security
- **Firewall**: Restrictive rules (backup and monitoring only)
- **SSH Keys**: Key-based authentication
- **VPN Access**: Netbird mesh for remote monitoring
- **Isolation**: Limited network access for security

## Performance Characteristics

### Backup Performance
- **HDD Pool**: ~80-120 MB/s sustained write
- **SSD Pool**: ~200-400 MB/s for fast recovery data
- **Network**: 1GbE (~110 MB/s theoretical maximum)
- **Bottleneck**: Usually network bandwidth

### Monitoring Performance
- **Query Response**: Sub-second Grafana dashboard loading
- **Data Retention**: 1 year of detailed metrics
- **Alert Latency**: <30 seconds for critical alerts
- **Dashboard Updates**: 30-second refresh rate

## Power & Thermal

### Power Consumption
- **Idle**: ~40W (drives spun down)
- **Backup Operations**: ~60W (all drives active)
- **Average**: ~45W (mixed workload)
- **Annual**: ~395kWh (@45W average)

### Thermal Management
- **Case Ventilation**: SFF optimized airflow
- **Drive Cooling**: Adequate for enterprise drives
- **CPU Cooling**: Stock cooler sufficient
- **Ambient**: Standard office environment

## Why This Configuration?

### Role Specialization
**Backup-focused design:**
- **Reliability**: ZFS mirrors on all storage
- **Capacity**: Adequate for lab backup needs
- **Monitoring**: Central oversight of entire lab
- **Cost-effective**: Reused hardware minimizes cost

### Storage Strategy
**Multiple backup tiers:**
- **Fast recovery**: SSD mirror for quick restores
- **Bulk storage**: HDD mirror for capacity
- **Offline protection**: USB drive for air-gap backup
- **Boot redundancy**: Mirror prevents single point of failure

### Monitoring Centralization
**Single pane of glass:**
- **Unified dashboards**: All lab metrics in one place
- **Historical data**: Trend analysis and capacity planning
- **Proactive alerts**: Issues identified before failure
- **Remote access**: Monitor lab health from anywhere

## Backup Strategy Implementation

### 3-2-1 Backup Rule
- **3 Copies**: Original + Server D + USB offline
- **2 Different media**: Network storage + USB drive
- **1 Offsite/Offline**: USB drive stored securely

### Replication Schedule
| Source | Target | Frequency | Retention |
|--------|--------|-----------|-----------|
| Server A Main | Server D HDD | Daily | 30 days |
| Server A Fast | Server D SSD | Daily | 30 days |
| Server D All | USB 6TB | Quarterly | 12 months |

### Recovery Testing
- **Monthly**: Automated restore verification
- **Quarterly**: Full recovery simulation
- **Documentation**: Recovery procedures updated

## Budget Breakdown

### Hardware Costs
| Component | Cost | Source | Status |
|-----------|------|---------|--------|
| HP EliteDesk 800 G4 SFF | €144 | Backmarket | ✅ Acquired |
| 16GB RAM (2×8GB) | €0 | Recovery | ✅ Available |
| Boot NVMe (2×250GB) | €0 | Recovery | ✅ Available |
| Archive HDD (2×4TB) | €0 | Synology recovery | ✅ Available |
| Fast SSD (2×1TB) | €0 | Server A transfer | ✅ Available |
| PCIe SATA Controller | €35 | - | ✅ Acquired |
| Drive mounting hardware | €20 | - | ✅ Acquired |
| USB 6TB drive | €0 | Existing | ✅ Available |

### Total Investment
**Server D Total**: **€199**
- **Hardware**: €199
- **Storage**: €0 (all recovered/transferred)
- **ROI**: Excellent for comprehensive backup solution

## Maintenance & Operations

### Regular Tasks
- **Weekly**: Review backup success/failures
- **Monthly**: ZFS scrub on all pools
- **Quarterly**: Drive SMART analysis
- **Annually**: Full recovery test

### Monitoring Alerts
- **Critical**: Drive failures, backup failures
- **Warning**: High disk usage, temperature alerts
- **Info**: Successful backups, system updates

### Capacity Planning
- **Growth tracking**: Monitor storage usage trends
- **Expansion planning**: Prepare for capacity increases
- **Hardware lifecycle**: Track drive ages and performance

## Integration with Lab

### Data Sources
- **Server A**: Primary replication source
- **Server B**: VM backup configs
- **Server C**: Service configurations
- **Network gear**: SNMP monitoring

### Alerting Integration
- **Email**: Backup status notifications
- **Mobile**: Critical alert push notifications
- **Dashboard**: Visual status indicators
- **Logs**: Detailed event logging

### Disaster Recovery
- **Documentation**: Complete recovery procedures
- **Priorities**: Critical service restore order
- **Testing**: Regular DR drills
- **Communication**: Incident response procedures

## Future Expansion

### Storage Growth
- **HDD Upgrade**: Replace 4TB with larger drives
- **SSD Expansion**: Add more fast recovery storage
- **USB Backup**: Upgrade to larger offline backup drive

### Monitoring Enhancement
- **Additional Metrics**: More detailed application monitoring
- **Longer Retention**: Extended historical data
- **Advanced Analytics**: Predictive failure analysis

### Network Upgrade
- **2.5GbE**: If backup windows become constrained
- **Dedicated Backup Network**: Isolated replication network

---

*Server D serves as the guardian of the lab - ensuring data safety, monitoring system health, and providing the confidence to experiment and innovate knowing that everything is safely backed up.* 🛡️

## Recovery Confidence

With Server D in place, the lab achieves:
- **Data Protection**: Multiple backup layers
- **System Visibility**: Complete monitoring coverage
- **Quick Recovery**: Fast restoration capabilities
- **Peace of Mind**: Comprehensive safety net

**"The best backup is the one you never need, but always have."** 💪
