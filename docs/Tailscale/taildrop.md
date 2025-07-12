# File Transfer via Taildrop

<a href="https://tailscale.com/kb/1106/taildrop" target="_blank">Official Documentation</a>

The steps below are for quickly sending a file from a Windows host to a remote Linux host while both are connected via Tailscale.

Transferring files between nodes on your Tailnet is possible between many/most platforms and OSes. Most of the time this is as simple as sharing a file from your Android or iOS device and selecting the Tailscale app as the destination, where you will be prompted to connect to your Tailnet if not connected already, and will then be able to select a device that is currently online and connected to the Tailnet.

## Commands to be run on Windows/local machine

1. Identify the file you would like to send/copy to the remote host.
2. Open a Windows Terminal/PowerShell session and change directory to the location where the file is stored.
3. Run the following command to send the file in question to the remote host:
    ```powershell
    tailscale file cp screenshot.jpg remote-host-tailscale-name:
    ```

    !!! Note
        The colon at the end of the command is necessary to delineate between a file and machine name.

## Commands to be run on the Linux/remote machine

1. Once the transfer is complete, change directory to the location where you want the file to be downloaded.
2. Run the following command to receive/retrieve the file to the current directory:

    ```bash
    sudo tailscale file get .
    ```

    !!! note
        The period can be replaced with a full directory if you don't want to navigate to the correct directory beforehand.

3. Run the `ls` command to verify the file is present.
