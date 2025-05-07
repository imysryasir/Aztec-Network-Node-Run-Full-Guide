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



## Software Requirements for VPS Users ( Only for VPS Users to Download Docker)

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







# Aztec Network Sequencer Node Run Full Guide (PC and VPS)

### Offical Docs Guide - https://docs.aztec.network/next/the_aztec_network/guides/run_nodes/how_to_run_sequencer



1️⃣ Dependencies for WINDOWS & LINUX & VPS
```
sudo apt-get update && sudo apt-get upgrade -y
```
```
sudo apt install curl iptables build-essential git wget lz4 jq make gcc nano automake autoconf tmux htop nvme-cli libgbm1 pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev  -y
```

2️⃣ Install Aztec Tools
```
bash -i <(curl -s https://install.aztec.network)
```
![440142117-610b5091-e8d5-45ac-9c9d-de26d080196e](https://github.com/user-attachments/assets/172299e5-9562-498e-a3af-420618cc6886)

3️⃣ Add Aztec to PATH
```
echo 'export PATH="$HOME/.aztec/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

Check version 
```
aztec
```

![440142705-be70b89b-e644-4d75-9087-1352cd544ad5](https://github.com/user-attachments/assets/fd5b6f95-e248-49cd-a188-0d573136e667)

Update version 
```
aztec-up alpha-testnet
```

4️⃣ Obtain RPC URLs

### Sepolia RPC URL (I use Alchemy)
* We need to create a Sepolia Alchemy RPC  --- Visit [here](https://dashboard.alchemy.com/)
* Login/Sign Up
* Click on `Create New app`
![Screenshot 2025-05-07 112101](https://github.com/user-attachments/assets/985af9c3-35cb-4eb9-afba-b32f6b886315)

* Give a name, Select Ethereum and `Create App`
* Click on `Network` tab and select Sepolia
![image](https://github.com/user-attachments/assets/c2eee62c-ec39-450c-aed8-e2a2eb5deee0)
* Copy the RPC, will be needed soon

-----
### Beacon RPC/L1 Consensus   

* Use:   `https://rpc.drpc.org/eth/sepolia/beacon`
 OR
* Use:    `https://lodestar-sepolia.chainsafe.io`

5️⃣ Check IP (for Local PC)
```
curl ipinfo.io/ip
```
```
curl ifconfig.me
```
Copy the IP, will be needed soon

6️⃣ Enable Firewall & Open Ports
```
sudo ufw allow ssh
sudo ufw enable

sudo ufw allow 40400
sudo ufw allow 40500
sudo ufw allow 8080
```

For VPS Only
```
apt install screen -y
```
```
screen -S aztecSequencer
```
- PRESS CTRL+A+D (to run ur node continuously)
- To check ur Node Again
```
screen -r aztecSequencer
```

7️⃣ Start Node
```
aztec start --node --archiver --sequencer \
  --network alpha-testnet \
  --l1-rpc-urls RPC_URL  \
  --l1-consensus-host-urls BEACON_URL \
  --sequencer.validatorPrivateKey YourPrivateKey \
  --sequencer.coinbase YourevmAddress \
  --p2p.p2pIp IP
  --p2p.maxTxPoolSize 1000000000
```

Replace the following variables before you Run Node:
* `RPC_URL` & `BEACON_URL`: Step 4
* `YourPrivateKey`: Your EVM wallet private key (with 0x prefix)
* `YourAddress`: Your EVM wallet public address
* `IP`: Your server IP (Step 5)

After entering the command, your node starts running, It takes a few hours for your node to get sync to the tip of the block and mostly depend on how powerful your device is.

##  Getting Apprentice Role on Discord

Make sure the Node is Synced to the tip - [Confirm from here](https://aztecscan.xyz/)

![image](https://github.com/user-attachments/assets/cea509d2-d0fe-4345-a32b-a9d18da4a3cb)

and compare with the Node

![image](https://github.com/user-attachments/assets/19b73911-3855-4795-baa8-8a2bf643e463)


+ Open a new Ubuntu screen (Make sure the Node is already running).

*Step 1: Get the latest proven block number:*
```bash
curl -s -X POST -H 'Content-Type: application/json' \
-d '{"jsonrpc":"2.0","method":"node_getL2Tips","params":[],"id":67}' \
http://localhost:8080 | jq -r ".result.proven.number"
```
* Save this block number for the next steps
* Example output: 23546

**Step 2: Generate your sync proof**
```bash
curl -s -X POST -H 'Content-Type: application/json' \
-d '{"jsonrpc":"2.0","method":"node_getArchiveSiblingPath","params":["BLOCK_NUMBER","BLOCK_NUMBER"],"id":67}' \
http://localhost:8080 | jq -r ".result"
```
* Replace 2x `BLOCK_NUMBER` with your number, the output from step1 above

![440303878-b6479b17-b94f-4914-9320-66d6b0afd0e5](https://github.com/user-attachments/assets/0d4e2512-1557-42a6-8ec7-1423bb744c78)

**Step 3: Register with Discord**
* Type the following command in this Discord server: `/operator start`
* After typing the command, Discord will display option fields that look like this:
* `address`:            Your validator address (Ethereum Address)
* `block-number`:      Block number for verification (Block number from Step 1)
* `proof`:             Your sync proof (base64 string from Step 2)

* Once you paste the proof, ensure your cursor is out of the proof details before you click on send to avoid the send button adding a gap to the details which will invlidate your proof

* After submission, you'll get your `Apprentice` Role


https://github.com/user-attachments/assets/7359be63-62bb-4951-8624-7175bd2a2bf0

  * Visit the [Discord channel](https://discord.com/invite/aztec)
  * Follow the Video guide
  * Start the `Operator` with the `/operator start` then select follow the video guide

--------

## Register as Validator
```
aztec add-l1-validator \
  --l1-rpc-urls SEPOLIA-RPC-URL \
  --private-key YOUR-PRIVATE-KEY \
  --attester YOUR-VALIDATOR-ADDRESS \
  --proposer-eoa YOUR-VALIDATOR-ADDRESS \
  --staking-asset-handler 0xF739D03e98e23A7B65940848aBA8921fF3bAc4b2 \
  --l1-chain-id 11155111
```
Replace `SEPOLIA-RPC-URL` , `YOUR-PRIVATE-KEY` , `YOUR-VALIDATOR-ADDRESS` with actual value and then then proceed it

## 🔶For Next Day Run This Command (Windows)

#1 Open WSL and Put this Command 
```
aztec start --node --archiver --sequencer \
  --network alpha-testnet \
  --l1-rpc-urls RPC_URL  \
  --l1-consensus-host-urls BEACON_URL \
  --sequencer.validatorPrivateKey YourPrivateKey \
  --sequencer.coinbase YourevmAddress \
  --p2p.p2pIp IP
  --p2p.maxTxPoolSize 1000000000
```

Replace the following variables before you Run Node:
* `RPC_URL` & `BEACON_URL`: Step 4
* `YourPrivateKey`: Your EVM wallet private key (with 0x prefix)
* `YourAddress`: Your EVM wallet public address
* `IP`: Your server IP (Step 5)

## Delete Node File
```
rm -r /root/.aztec
```

## Need to Free Your 8080 Port

### Identify the Process Using Port 8080
```
sudo ss -tulpn | grep 8080
```

Example - ``` LISTEN  0  128  0.0.0.0:0380  0.0.0.0:*  users:(("nginx",pid=1234,fd=6)) ```

### Terminate the Process by PID
```
sudo kill -9 1234
```

### Kill All Processes Using Port 8080
```
sudo fuser -k 8080/tcp
```

Reference Video How to Free 8080 or any port - https://youtu.be/4iP4GvLfCrU?t=229
