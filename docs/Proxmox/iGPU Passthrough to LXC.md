# iGPU Passthrough to LXC

## Setting up fstab to auto-mount NAS shares via SMB/CIFS

1. Install Jellyfin via Proxmox Helper Scripts
2. Select custom installation and be sure the container is created as privileged vs. unprivileged so the NFS/CIFS mounts and hardware transcoding can work properly.
3. Power the LXC container down to make modifications 3. Go to Options > Features and click Edit
4. Add NFS, SMB/CIFS as needed
5. Power on the LXC container
6. Install CIFS Utils and/or NFS Utils (use sudo if not logged in as root user)

    ```bash
    bash apt install cifs-utils nfs-common
    ```

7. Edit the fstab

    ```bash
    nano /etc/fstab
    ```

8. Go to the first blank/open line and enter the following:

    ```bash
    # CIFS/SMB Mount
    # //192.168.2.6/Media     /mnt/media      cifs    user=jellyfin,password=jellyfin,iocharset=utf8,noperm   0       0
    # NFS Mount
    192.168.2.6:/mnt/user/Media     /mnt/media      nfs     rw,hard 0       0
    ```

9. Save changes to the fstab

---

## Configuration to pass through iGPU

https://jellyfin.org/docs/general/administration/hardware-acceleration/intel#lxc-on-proxmox

1. Load the correct graphics driver for the container

    ```bash
    nano /etc/modprobe.d/i915.conf
    ```

2. Add the following line to the blank file and save:

    ```bash
    options i915 enable_guc=3
    ```

3. Modify the LXC container's config file where the ###.conf is the ID of the container

    ```bash
    nano /etc/pve/lxc/101.conf
    ```

4. Add the following lines to the end of the container config (the Proxmox Helper Script may have added these lines already - no need to add them 2x if they are already there):

    ```bash
    lxc.cgroup2.devices.allow: c 226:0 rwm 
    lxc.cgroup2.devices.allow: c 226:128 rwm 
    lxc.mount.entry: /dev/dri/renderD128 dev/dri/renderD128 none bind,optional,create=file
    ```

5. Pass through the iGPU

    ```bash 
    chmod -R 777 /dev/dri/*
    ```

6. Verify the passthrough in the Jellyfin LXC

    ```bash
    ls /dev/dri
    ```

7. Install drivers in the container

    ```bash
    apt install vainfo intel-gpu-tools
    ```
8.  Verify driver install status and supported codecs by running the `vainfo` command and `intel_gpu_top`
9.  Make sure user and group settings are correct

    ```bash
    usermod -aG video jellyfin usermod -aG input jellyfin usermod -aG render jellyfin
    ```
10. Restart the Jellyfin service for changes to take effect

    ```bash
    systemctl restart jellyfin.service
    ```
11. Select Intel QSV/QuickSync transcoding in the dropdown and select the correct codecs. 
  - Depending on the generation of Intel CPU/iGPU you are using, you may/will likely need to enable both low power modes.
12. To configure and verify low power (LP) mode, install the following:

    ```bash
    apt update && apt install -y linux-firmware
    ```

13. Add the following to the host system to enable loading of GuC and HuC low power firmwares: 

    ```bash
    mkdir -p /etc/modprobe.d sh -c "echo 'options i915 enable_guc=2' >> /etc/modprobe.d/i915.conf"
    ```

14. Update the initramfs and grub

    ```bash
    update-initramfs -u && update-grub
    ```

15. Reboot the system for the changes to take effect
16. Verify the firmware status and be sure there is no ERROR or FAIL in the output

    ```bash
    dmesg | grep i915 cat /sys/kernel/debug/dri/0/gt/uc/guc_info cat /sys/kernel/debug/dri/0/gt/uc/hu`_info`
    ```

    or FAIL in the output 

    ```bash
    dmesg | grep i915 cat /sys/kernel/debug/dri/0/gt/uc/guc_info cat /sys/kernel/debug/dri/0/gt/uc/hu
    ```
