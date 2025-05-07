Aztec-Network-Node-Run-Full-Guide| & | System Requirements.

# Hardware Requirements 

## Overview

| Component      | Specification                      |
|----------------|------------------------------------|
| CPU            | 8 core Processor                   |
| RAM            | 16 GB (6–8 GB can also run it)     |
| Storage        | 100 GB SSD                         |
| Internet Speed | 25 Mbps Upload / Download          |


> [!Note]
> **You can start running this node on a `4-core CPU`, `6 GB of RAM` and `25 GB of storage`. However, as uptime increases, it's important to meet the recommended system requirements—otherwise, your node may eventually crash.**

## 🌐 Rent VPS
> [!Note]
> **Renting VPS is not necessarily needed if your main goal is to take `Apprentice` role on Aztec Discord, You can run this node on WSL for 30-60 mins to get that role**

# Software Requirements for PC Users

1. For Windows Install WSL - https://learn.microsoft.com/en-us/windows/wsl/install#install-wsl-command
2. For Windows Install Ubuntu after Installing WSL - https://apps.microsoft.com/detail/9PDXGNCFSCZV?hl=en-us&gl=IN&ocid=pdpshare
3. Install Docker - https://www.docker.com/products/docker-desktop/

## Software Requirements for VPS Users (Additional Only for VPS Users to Download Docker)

```
sudo apt update -y
```
```
sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
```
```
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```
```
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
```
sudo apt update -y
```
```
apt-cache policy docker-ce
```
```
sudo apt install docker-ce -y
```
```
sudo usermod -aG docker ${USER}
su - ${USER}
groups
```
