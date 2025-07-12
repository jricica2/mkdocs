# Enable Tailscale SSH

<a href="https://tailscale.com/kb/1193/tailscale-ssh" target="_blank">Official Documentation</a>

The steps below are for enabling quick SSH access to a machine on your Tailnet without the need to manually copy SSH keys from one machine to another.

1. Configure and install Tailscale on the machine as you normally would/already have based on the host OS.

2. Run the following command:

    ```bash
    tailscale set --ssh
    ```

3. If you are currently connected to the machine via Tailscale, you will be prompted to add the `--accept-risk=lose-ssh` flag to the command in order for it to be successful.

    ```bash
    tailscale set --ssh --accept-risk=lose-ssh
    ```

4. If you lose SSH, simply re-initiate the connection `ssh admin@machine` and it should not prompt for a password.


5. If you did not lose SSH, close and re-connect using the Tailscale DNS name or IP address and it should not prompt for a password.
