# 02 – Networking Configuration

## Overview

Three Linux bridges were configured on the Proxmox host:

| Bridge | Purpose              | Subnet / Mode     |
|--------|----------------------|-------------------|
| vmbr0  | Management           | Bridged to host   |
| vmbr1  | Production / Server  | 10.10.10.0/24     |
| vmbr2  | Test / Lab           | 10.20.20.0/24     |

## Bridge Configuration

### vmbr0 – Management

- Type: Linux Bridge
- Bridge ports: physical NIC (or VMware network adapter)
- IP: assigned by the physical/host network (or static)
- Used for Proxmox web UI and SSH access

### vmbr1 – Server Network

- Type: Linux Bridge
- IP address: `10.10.10.1/24`
- No gateway (isolated network)
- Used by production VMs (`web-prod-01`, `db-prod-01`)

### vmbr2 – Test Network

- Type: Linux Bridge
- IP address: `10.20.20.1/24`
- No gateway (isolated network)
- Used by test VMs (`app-test-01`, `mon-test-01`)

