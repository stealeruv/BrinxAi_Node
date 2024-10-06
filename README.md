# BrinxAi Worker and Relay Node Detailed Setup Guide

BrinxAI is Ai-DePIN project that aims to revolutionize the AI tools landscape by leveraging the power of decentralized networks and cryptocurrency incentives. To  create a robust ecosystem that rewards node operators, supports third-party developers, and caters to various user needs including students, developers, and those with reading difficulties.

Docs : [BrinxAi docs](https://brinxai.gitbook.io/brinxai-depin-ai) | X : [BrinxAi](https://x.com/BrinxAi_Labs)

Node Operators : 

- Revenue Sharing: Operators earn cryptocurrency rewards for maintaining and operating nodes.

- Staking Mechanism: Operators stake tokens to run nodes, ensuring commitment and network stability.

# Join Crypto Console Community

Join TG : [Crypto Console Telegram](https://t.me/cryptoconsol) 

Follow X : [Crypto Console Twitter](https://www.x.com/cryptoconsol) 

Subscribe : [Crypto Console Youtube](https://www.youtube.com/@cryptoconsole)

--

VPS Options:

Credit Card/Paypal : 

VPS 1 : [Contabo: Cloud VPS 1](https://www.jdoqocy.com/click-101278318-15692486)

VPS 2 : [Contabo: Cloud VPS 2](https://www.tkqlhce.com/click-101278318-13796472)

VPS 3 : [Contabo: Cloud VPS 3](https://www.dpbolvw.net/click-101278318-13796474)

VPS 4 : [Contabo: Cloud VPS 3](https://www.anrdoezrs.net/click-101278318-13796476)


Crypto payment : [https://vpsdime.com](https://vpsdime.com/a/4418/linux-vps)

## 1.Update and Install Dependencies
```
sudo apt update && sudo apt upgrade
sudo apt-get install ca-certificates curl
```

### Install Docker

Setup Docker Rep

```
# Add Docker's official GPG key:
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

### Docker Setup

```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
### Check
```
docker --version
```
### Install Docker Compose
```
VER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep tag_name | cut -d '"' -f 4)

curl -L "https://github.com/docker/compose/releases/download/"$VER"/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

chmod +x /usr/local/bin/docker-compose
docker-compose --version
```
### Setup Docker permission
```
sudo groupadd docker
sudo usermod -aG docker $USER
```

## 2.Worker Node Setup

Pull Worker Image from Docker Hub

```
docker pull admier/brinxai_nodes-worker:latest
```
### Install NVIDIA Drivers for Docker (optional)

Follow the guide below before proceeding if you want GPU Enabled.

```
curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg \
  && curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list | \
    sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
    sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list
```
```
sed -i -e '/experimental/ s/^#//g' /etc/apt/sources.list.d/nvidia-container-toolkit.list
sudo apt-get update
sudo apt-get install -y nvidia-container-toolkit
sudo nvidia-ctk runtime configure --runtime=docker
sudo systemctl restart docker
```


## 3.Install UFW firewall : 
```
sudo apt-get install ufw
```

### Allow the port 5011:

```
sudo ufw allow 5011/tcp
```
### Enable UFW:

```
sudo ufw enable
```
### Verify the UFW status:

```
sudo ufw status
```

### Run Worker Docker Image

```
git clone https://github.com/admier1/BrinxAI-Worker-Nodes
cd BrinxAI-Worker-Nodes
chmod +x install_ubuntu.sh
./install_ubuntu.sh
```

# Relay Node Steup
```
sudo ufw allow 1194/udp
```

### Check Processor
```
uname -m
```
Run the Relay Image

AMD64:

```
sudo docker run -d --name brinxai_relay --cap-add=NET_ADMIN -p 1194:1194/udp admier/brinxai_nodes-relay:latest
```
ARM64:

```
sudo docker run -d --name brinxai_relay --cap-add=NET_ADMIN -p 1194:1194/udp admier/brinxai_nodes-relay:arm64
```


Register Your Relay Node

- Visit workers.brinxai.com.

- Create an account using your email and password.

- Log in to your account.

- Give any node name and enter your vps IP address
