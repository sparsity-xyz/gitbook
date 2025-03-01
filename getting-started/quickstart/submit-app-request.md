---
description: App Smart Contract Initialization
---

# Submit App Request

## 1. Deploy and Test Your Smart Contract Locally

### 1.1 Deploying the Contract Locally

Let's deploy and run the contract locally to ensure everything functions as expected.

#### Prerequisites

Before proceeding, ensure that **Foundry** is installed to run a local blockchain:

🔗 **[Foundry Installation Guide](https://book.getfoundry.sh/getting-started/installation)**

#### Deployment Steps

**1️⃣ Navigate to the Contract Directory**

```sh
cd contract
```

**2️⃣ Install packages**

```sh
npm install
```

**3️⃣ Copy and Configure the Environment Variables**

```sh
cp .env.example .env
```

By default, the following contract addresses are used:

```sh
APP_CONTRACT=0x5FbDB2315678afecb367f032d93F642f64180aa3  # Default App contract address  
OUTPOST_PROXY_CONTRACT=0xe7f1725E7734CE288F8367e1Bb143E90bb3F0512  # Default mock Sparsity Outpost address
DEPLOYER_PRIVATE_KEY=0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80  # Default test private key for deployment
```

**4️⃣ Start a Local Blockchain Node**

```sh
pkill -f anvil || true
nohup anvil > anvil.log 2>&1 &
MAKE deploy
tail -f anvil.log
```

Alternatively, you can simply run:

```sh
make node
```

The output of Deployed Addresses 
```
APPModule#APP - 0x5FbDB2315678afecb367f032d93F642f64180aa3
```

***

### 1.2 Generating Initial Data for the Sparsity Network

Let's take an example where we want to compute `fibonacci(22)` using the **Sparsity Network**.

#### Understanding Initial Data

The **App Smart Contract** generates ABI-encoded data and sends it to the **Sparsity Network**.\
This encoded data will be used in the next step for **App ABCI Core** setup and verification.

#### Generating Initial Data

To generate ABI-encoded data for `fibonacci(22)`, run the following command:

```sh
export APP_CONTRACT=0x5FbDB2315678afecb367f032d93F642f64180aa3
export DEPLOYER_PRIVATE_KEY=0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80
export NUM=22

cast send ${APP_CONTRACT} --private-key ${DEPLOYER_PRIVATE_KEY} "requestFib(uint256)" ${NUM}
RAW_DATA=$(cast call "${APP_CONTRACT}" "initialData(uint256)" "22") && cast abi-decode "initialData(uint256)(bytes)" "$RAW_DATA"
```

Or simply run:

```sh
make request-fib NUM=22
```

This command outputs the ABI-encoded input data on the last line, which will be used in the **ABCI Core setup validation** in the next steps:

```sh
0x0000000000000000000000000000000000000000000000000000000000000016
```
