# Naming Convention

## Virtual Machines

| VMID | Name           | Role                  | Network | Notes                  |
|------|----------------|-----------------------|---------|------------------------|
| 100  | tpl-debian12   | Template              | vmbr0   | Debian 12 base template |
| 101  | web-prod-01    | Production Web Server | vmbr1   |                        |
| 102  | db-prod-01     | Production Database   | vmbr1   |                        |

## Networks

| Bridge | Name            | Subnet          | Purpose              |
|--------|-----------------|-----------------|----------------------|
| vmbr0  | Management      | Bridged         | Proxmox management   |
| vmbr1  | Server Network  | 10.10.10.0/24   | Production VMs       |
| vmbr2  | Test Network    | 10.20.20.0/24   | Test / Lab VMs       |

## Storage

| Name            | Type     | Path / Backend     | Purpose              |
|-----------------|----------|--------------------|----------------------|
| local           | Directory| /var/lib/vz        | ISOs, templates      |
| local-lvm       | LVM-Thin | pve/data           | VM disks             |
| backup-storage  | Directory| /mnt/backup        | VZDump backups       |