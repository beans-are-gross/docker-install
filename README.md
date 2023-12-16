# Simple Docker Install for Ubuntu

[This, but simple](https://docs.docker.com/engine/install/ubuntu/)

## Docker Install

```terminal
sudo apt-get update && apt-get install ca-certificates curl gnupg lsb-release -y
sudo mkdir -p /etc/apt/keyrings && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

> **If you get a GPG error:**
> ```terminal
> sudo chmod a+r /etc/apt/keyrings/docker.gpg
> sudo apt-get update
> ```

**Else:**

```terminal
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin -y
sudo usermod -aG docker $USER
```

# Docker Container Controllers

## Dockge (great for beginners)
```terminal
apt update && apt install curl
mkdir -p /opt/stacks /opt/dockge
cd /opt/dockge
curl "https://dockge.kuma.pet/compose.yaml?port=5001&stacksPath=%2Fopt%2Fstacks" --output compose.yaml
docker compose up -d
```

## Portainer (great for more info)
```terminal
docker volume create portainer_data
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```

> **If you were timed out when signing up, run this command:**
> ```terminal
> docker container restart portainer
> ```

## Portainer Agent
```terminal
docker run -d -p 9001:9001 --name portainer_agent --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v /var/lib/docker/volumes:/var/lib/docker/volumes portainer/agent:2.16.2
```

## Yacht
```terminal
docker volume create yacht
docker run -d -p 8001:8000 --name yacht --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v yacht:/config selfhostedpro/yacht 
```

> **Important:** This is the default login information:
> - Username: admin@yacht.local
> - Password: pass
