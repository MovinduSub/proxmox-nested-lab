# Proxmox Nested Lab

A nested Proxmox VE lab running inside VMware Workstation for learning virtualization, networking, templates, and backup/restore.

## Lab Overview

- **Host**: VMware Workstation
- **Hypervisor**: Proxmox VE (nested)
- **Purpose**: Practice VM templating, isolated networks, automated backups, and recovery testing

## Architecture

### Networks

| Bridge | Name             | CIDR            | Purpose                    |
|--------|------------------|-----------------|----------------------------|
| vmbr0  | Management       | Bridged         | Proxmox management access  |
| vmbr1  | Server Network   | 10.10.10.0/24   | Production VMs             |
| vmbr2  | Test Network     | 10.20.20.0/24   | Test / experimental VMs    |

### Storage

| Storage         | Type      | Location          | Purpose                |
|-----------------|-----------|-------------------|------------------------|
| local           | Directory | /var/lib/vz       | ISOs & templates       |
| local-lvm       | LVM-Thin  | pve/data          | VM disks               |
| backup-storage  | Directory | /mnt/backup       | Automated backups      |

### Virtual Machines

| VMID | Name           | Role                     | Network | Status     |
|------|----------------|--------------------------|---------|------------|
| 100  | tpl-debian12   | Debian 12 Template       | vmbr0   | Template   |
| 101  | web-prod-01    | Production Web Server    | vmbr1   | Active     |
| 102  | db-prod-01     | Production Database      | vmbr1   | Active     |

## Completed Steps

- [x] Proxmox VE installed nested in VMware Workstation
- [x] Second disk added and mounted as `/mnt/backup`
- [x] Networks created (`vmbr0`, `vmbr1`, `vmbr2`)
- [x] Debian 12 template created with qemu-guest-agent + cloud-init
- [x] Production VMs cloned from template
- [x] Automated backup job configured to `backup-storage`
- [x] Full VM restore tested

## Backup & Recovery

- **Backup Storage**: `backup-storage` (`/mnt/backup`)
- **Backup Mode**: Snapshot + ZSTD compression
- **Retention**: Configurable (currently keeping multiple versions)
- **Recovery Tests**:
  - Full VM restore: Successful
  - File-level restore: (to be documented)

## Naming Convention

See [NAMING.md](NAMING.md)

## How to Use This Lab

1. Clone the template (`tpl-debian12`) for new VMs
2. Attach the correct network bridge (`vmbr1` for production, `vmbr2` for testing)
3. Backups run automatically according to the configured schedule
4. Restore from `backup-storage` when needed

## Notes

- This is a nested lab — performance is limited by the underlying VMware host.
- Always prefer clean shutdowns to avoid filesystem issues.
- Thin pool space on `local-lvm` should be monitored regularly.