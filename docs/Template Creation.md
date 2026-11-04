# 03 – Debian Template Creation

## Goal

Create a clean, reusable Debian 12 template with:

- `qemu-guest-agent` installed
- `cloud-init` installed and cleaned
- Machine-specific identifiers removed

## Steps Performed

### 1. Create and Install the VM

1. Uploaded Debian 12 ISO to Proxmox storage (`local`)
2. Created a new VM
3. Attached the ISO and completed a standard Debian installation
4. Installed `sudo` and basic packages as needed

### 2. Install Required Packages

```bash
apt update
apt install -y qemu-guest-agent cloud-init
systemctl enable qemu-guest-agent
systemctl start qemu-guest-agent



Clean the System for Templating
# Clean cloud-init
cloud-init clean --logs

# Remove SSH host keys
rm -f /etc/ssh/ssh_host_*

# Clear machine-id
truncate -s 0 /etc/machine-id
rm -f /var/lib/dbus/machine-id

# Optional: clear apt cache and logs
apt clean
journalctl --vacuum-time=1s



Power Off and Convert to Template
Shutdown the VM cleanly
In Proxmox GUI: right-click the VM → Convert to Template
Rename to tpl-debian12 (VMID 100)


