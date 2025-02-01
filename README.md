# Prerequisites

Before you begin running your **zkVerify** node, ensure that you have the following installed on your machine:

- Docker,
- Docker Compose (v2),
- `jq` tool,
- `gnu-sed` tool (macOS only).
 
# Hardware Requirements

The hardware requirements are listed in the table below:

| Requirement        | RPC node           | Boot node          | Validator node     |
| ------------------ | ------------------ | ------------------ | ------------------ |
| Core               | 1                  | 1                  | 1                  |
| Threads per core   | 2                  | 2                  | 2                  |
| Clock speed (GHz)  | 2.2                | 2.2                | 2.2                |
| Memory (GiB)       | 2                  | 4                  | 2                  |
| Bandwidth (Gigabit)| Up to 5            | Up to 5            | Up to 5            |
| Storage (GB)       | 50<br/>5 with pruning| 5                | 150                |

# Node Setup 

## 1. Persiapan Awal
```
sudo apt update && sudo apt install -y docker.io docker-compose jq sed
```

Tambahkan user Anda ke grup Docker:
```
sudo usermod -aG docker $USER
newgrp docker
```

Cek apakah Docker sudah terinstal 
```
docker ps
```
## 2. Membuat User Khusus untuk Node
```
sudo useradd -m -s /bin/bash zkverify
sudo passwd zkverify
sudo usermod -aG docker zkverify
```

Beralih ke user zkverify:
```
su - zkverify
cd ~
```

## 3. Clone Repository dan Jalankan Skrip
```
git clone https://github.com/zkVerify/compose-zkverify-simplified.git
cd compose-zkverify-simplified
```

Jalankan skrip inisialisasi:
```
./scripts/init.sh
```

Pilih Validator-node

## 4. Start node:
```
./scripts/start.sh
```
```
docker compose -f /home/your_user/compose-zkverify-simplified/deployments/validator-node/testnet/docker-compose.yml up -d
```

## 5. Registrasi node ke blockchain :
Selanjutnya tutorial nya untuk konek ke polkadot ada di docs nya ya : 
- Tutor nya  : https://docs.zkverify.io/tutorials/how_to_run_a_node/run_using_docker/run_new_validator_node
- Connect wallet: https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Ftestnet-rpc.zkverify.io#/staking
- Faucet address subrate polkadot: https://zkverify-faucet.zkverify.io/
  
## 6. Monitoring 

- Cek docker:
```
docker container ls
```
- Cek logs:
```
docker logs -f validator-node
```
- Menghentikan atau Menghapus Node
```
./scripts/stop.sh
```
- Untuk menghapus node sampai akar-akar nya 
```
./scripts/destroy.sh
```
- Cek Node : https://testnet-telemetry.zkverify.io/#/0xc00425dcaa0a1bc5bf1163a2d69d7abb2cc6180de78b4e10297b31a4d9cc928a

