# 01 – Proxmox Installation & Storage Setup

## Nested Installation

Proxmox VE was installed as a nested virtual machine inside VMware Workstation.

### Key steps performed

1. Created a new VM in VMware Workstation for Proxmox
2. Enabled nested virtualization (VT-x/AMD-V) in the VM settings
3. Booted from the Proxmox VE ISO and completed the installation
4. Configured basic network and management access via `vmbr0`

## Extra Disk for Backups

A second virtual disk was added to the Proxmox VM and configured as backup storage.

### Steps

1. Added a new virtual disk in VMware Workstation
2. Inside Proxmox, identified the new disk (`/dev/sdb` or similar)
3. Partitioned and formatted the disk
4. Mounted it at `/mnt/backup`
5. Added it to Proxmox as a Directory storage named `backup-storage`

```bash
# Example commands (adjust device name as needed)
mkfs.ext4 /dev/sdb1
mkdir -p /mnt/backup
mount /dev/sdb1 /mnt/backup
echo '/dev/sdb1 /mnt/backup ext4 defaults 0 2' >> /etc/fstab