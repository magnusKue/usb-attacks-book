# Docker Deployment (Server)

The Sliver server is deployed as a containerized microservice. Since this configuration represents *Infrastructure as Code (IaC)*, the files are stored openly within the repository. The security relies entirely on cryptographic mutual TLS authentication, not on the secrecy of the deployment structure.

### 1. The Dockerfile
The Dockerfile is based on a clean Ubuntu image and automatically pulls and installs the latest stable server daemon from Bishop Fox.

```dockerfile
FROM ubuntu:22.04

RUN apt-get update && apt-get install -y \
    curl \
    wget \
    git \
    iproute2 \
    ca-certificates \
    && rm -rf /var/lib/apt/lists/*

# Automatically install the Sliver server binary
RUN curl -s [https://sliver.sh/install](https://sliver.sh/install) | bash

# Expose the default mTLS operator administration port
EXPOSE 31337

CMD ["/root/sliver-server", "daemon"]

```
### 2. Docker Compose Configuration

The `docker-compose.yml` file links the server daemon to our external proxy network and maps port 31337 exclusively to the host system's Tailscale network interface.

```yaml
version: "3.8"

services:
  sliver:
    build: .
    container_name: sliver-server
    restart: unless-stopped
    ports:
      - "31337:31337"
    volumes:
      - sliver-data:/root/.sliver
      - /tmp:/tmp
    networks:
      - proxy

volumes:
  sliver-data:

networks:
  proxy:
    external: true
```
### 3. Initializing the Server

To build the Docker image from scratch and launch the C2 daemon persistently in the background, run the following command inside your deployment directory:

```bash
$ docker compose up -d --build 
```
### 4. Generating the Operator Profile

Because Sliver relies entirely on mTLS for client connections, an operator profile containing unique X.509 certificates must be created inside the running container before any client can connect:

``` bash
$ docker exec -it sliver-server /root/sliver-server operator --name _your_name --lhost _your_IP --save /tmp/meinlaptop.cfg
```
