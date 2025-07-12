# Installing Portainer

## Portainer Installation

1.  Create the persistent volume to store Portainer data

    ```bash
    docker volume create portainer_data
    ```

2.  Install/run Portainer

    ```bash
    docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:2.21.4
    ```

### Updating Portainer

1.  Stop Portainer

    ```bash
    docker stop portainer
    ```

2.  Remove the existing Portainer image

    ```bash
    docker rm portainer
    ```

3.  Pull the newest version of Portainer

    ```bash
    docker pull portainer/portainer-ce:2.27.0
    ```

4.  Run the newly-pulled container

    ```bash
    docker run -d -p 8000:8000 -p 9443:9443 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:2.27.0
    ```
