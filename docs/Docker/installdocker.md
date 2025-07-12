# Installing Docker & Docker Compose

## Docker Installation

#### Recommend installing the Pi-Hosted version from Novaspirit Tech's Github repository

<a href="https://github.com/novaspirit/pi-hosted" target="_blank">https://github.com/novaspirit/pi-hosted</a>

!!! warning
    `curl` and/or `git` are not installed by default and will be required to run the script, either via the wget commands or by cloning the repository to your local machine.

1. Run the following command:
    ```bash
    # Script to install Docker
    wget -qO- https://raw.githubusercontent.com/pi-hosted/pi-hosted/master/install_docker.sh | bash
    ```

2. Reboot for changes to take effect

3. Run the following command:
    ```bash
    # To install Portainer
    wget -qO- https://raw.githubusercontent.com/pi-hosted/pi-hosted/master/install_portainer.sh | bash
    ```

    ```bash
    # To update Portainer
    wget -qO- https://raw.githubusercontent.com/pi-hosted/pi-hosted/master/update_portainer.sh | bash
    ```

4. Log into Portainer via port 9000
5. Click Settings in the lower left corner, and paste the appropriate link in the "App Templates" field:

    | Architecture | URL |
    | ------------ | --- |
    | ARM64 | `https://raw.githubusercontent.com/pi-hosted/pi-hosted/master/template/portainer-v3-arm64.json` |
    | AMD64 | `https://raw.githubusercontent.com/pi-hosted/pi-hosted/master/template/portainer-v3-amd64.json` |


---
## Official Docker Documentation

<a href="https://docs.docker.com/engine/install/ubuntu/" target="_blank">https://docs.docker.com/engine/install/ubuntu/</a>

## Add the Repository

```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

## Install Docker and Components

```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### Manage Docker via a non-root user

```bash
sudo groupadd docker
```

```bash
sudo usermod -aG docker $USER
```

Log out and log back in to verify changes

### Start Docker on system boot

```bash
sudo systemctl enable docker.service
sudo systemctl enable containerd.service
```
