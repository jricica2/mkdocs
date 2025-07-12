# Proxmox LXC Mounts

Output of /etc/fstab:

```bash
# UNCONFIGURED FSTAB FOR BASE SYSTEM
# //192.168.2.6/Media     /mnt/media      cifs    user=jellyfin,password=jellyfin,iocharset=utf8,noperm   0       0
# 192.168.2.6:/mnt/user/Media     /mnt/media      nfs     rw,hard 0       0
192.168.2.22:/Volume1/Media  /mnt/media  nfs  rw,hard  0  0
```