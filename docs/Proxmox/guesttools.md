# Proxmox Qemu-guest-agent Installation

<a href="https://pve.proxmox.com/wiki/Qemu-guest-agent" target="_blank">https://pve.proxmox.com/wiki/Qemu-guest-agent</a>

## Linux Guests

1. Install the qemu-guest-agent via the following commands:

    ```bash
    # Debian/Ubuntu-based Systems
    apt-get install qemu-guest-agent
    ```

    ```bash
    # Redhat-based systems
    yum install qemu-guest-agent
    ```

2. Start the guest agent manually if it did not start automatically

    ```bash
    systemctl start qemu-guest-agent
    ```

3. Enable the service to start automatically upon boot

    ```bash
    systemctl enable qemu-guest-agent
    ```

