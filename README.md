# OpenVAS Deployment
OpenVAS Deployment with CF Tunnel

## Deploy

### Set tunnel token

#### Option 1: Set environment variable

    export VENDITO_TUNNEL_TOKEN="<token>"

#### Option 2: Add .env file

Add .env file with and set the variable there. See .env.sample as an example.

### Download Docker compose files

    curl -f -L https://greenbone.github.io/docs/latest/_static/docker-compose-22.4.yml -o gvm-docker-compose.yml
    curl -f -L https://raw.githubusercontent.com/VenditoKft/OpenVASDeploy/main/tunnel.yml -o gvm-tunnel-compose.yml

For older docker compose, please comment out the ports line in gvm-tunnel-compose.yml after downloading it.
   
### Starting containers

#### Optionally pull images

    docker compose -f gvm-docker-compose.yml -f gvm-tunnel-compose.yml pull

#### Start the containers

    It will automatically pull the images as well if previous step was skipped.

    docker compose -f gvm-docker-compose.yml -f gvm-tunnel-compose.yml -p greenbone-community-edition up -d

## Destroy

    docker compose -p greenbone-community-edition down -v

## Misc commands

    docker compose -p greenbone-community-edition logs -f
    docker compose -p greenbone-community-edition exec -u gvmd gvmd gvmd --user=admin --new-password=<password>
    docker compose -p greenbone-community-edition exec <container-name> /bin/bash
