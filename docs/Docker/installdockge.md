# Installing Dockge

### Developer's GitHub

<a href="https://github.com/louislam/dockge" target="_blank">https://github.com/louislam/dockge</a>

1.  Create directories that store your stacks and stores Dockge's stack
    ```bash
    mkdir -p /opt/stacks /opt/dockge
    cd /opt/dockge
    ```

2.  Download the compose.yaml
    ```bash
    curl https://raw.githubusercontent.com/louislam/dockge/master/compose.yaml --output compose.yaml
    ```

3. Start the server
    ```bash
    docker compose up -d
    
    # If you are using docker-compose V1 or Podman
    docker-compose up -d
    ```

Dockge is now running on http://localhost:5001

### Advanced

If you want to store your stacks in another directory, you can generate your compose.yaml file by using the following URL with custom query strings.

```bash
# Download your compose.yaml
curl "https://dockge.kuma.pet/compose.yaml?port=5001&stacksPath=/opt/stacks" --output compose.yaml
```

- port=`5001`
- stacksPath=`/opt/stacks`

Interactive compose.yaml generator is available on: 

<a href="https://dockge.kuma.pet" target="_blank">https://dockge.kuma.pet</a>

## How to Update

```bash
cd /opt/dockge
docker compose pull && docker compose up -d
```
