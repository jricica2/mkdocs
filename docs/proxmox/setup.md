# Post-Installation

## Techno Tim's First 11 Things
---
1. Install updates
```bash
apt update && apt upgrade -y
```

2. Set up storage

3. Check S.M.A.R.T Status

4. Turn on PCIE passthrough (IOMMU)
```
nano /etc/default/grub
```
Add the following to the existing line:
```
GRUB_CMDLINE_LINUX_DEFAULT="quiet intel_iommu=on" 
```
Run the following commands:
```bash
update-grub
```
```bash
update-initramfs -u
```
Reboot the server for the changes to take effect
```bash
reboot now
```

5. Set up an NFS share for backups, isos, etc.

6. Set up backups

7. Upload the virtio ISO for Windows guests

8. Upload Windows and Linux ISO files

9. Create a Linux VM template and clone for use

10. Set up alerts

