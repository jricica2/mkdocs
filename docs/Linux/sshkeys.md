# SSH Keys

[https://www.linode.com/docs/guides/use-public-key-authentication-with-ssh/](https://www.linode.com/docs/guides/use-public-key-authentication-with-ssh/)

## Create SSH Key
1. Create an SSH key on the device you would like to connect from

    ```bash
    ssh-keygen
    ```

    ```bash
    # Recommended
    ssh-keygen -t ed25519
    ```

    ```bash
    ssh-keygen -t rsa -b 4096
    ```

2. Copy the newly-created key to the remote server

    ```bash
    ssh-copy-id username@remote_host
    ```

3. You will be prompted to authenticate with your password for the account in question. If successful, the key will be copied.
4. Try to connect to the remote host again.

    ```bash
    ssh username@remote_host
    ```

5.  If the previous steps were successful, you should be connected via the SSH key and not be prompted for password.

## Disable login for root account

1. Edit the sshd_config file in the text editor of your choice via the following command:

    ```bash
    sudo nano /etc/ssh/sshd_config
    ```

2. Locate the line that contains `#PermitRootLogin yes` and uncomment the # symbol and change the `yes` to `no` so it reads `PermitRootLogin no`
3. You can also set the line to `PermitRootLogin no-password` (I think) to only allow logon via SSH auth keys
4. Once root login has been disabled, you can make the change active by running any of the following commands:

    ```bash
    /etc/init.d/sshd restart
    systemctl restart sshd
    service sshd restart
    ```

