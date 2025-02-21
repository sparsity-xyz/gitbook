---
description: App ABCI Core Execution
---

# Execute App Computation

## 2. Running the ABCI Core Locally

To test the functionality of the ABCI Core, we can run it locally. The ABCI Core processes the initial data passed from the smart contract’s \[`newSession`] function, specifically the `initialData` input. This data is then injected into the Sparsity Ephemeral Rollup Network, enabling decentralized off-chain computation and acceleration.

### Example: Computing Fibonacci(22)

#### 1️⃣ Navigate to the Server Directory

First, move into the server directory:

```sh
cd server

npm install
```

#### 2️⃣ Preparing the Initial Data

The `INIT_DATA` is the ABI-encoded input sent from the smart contract.

For `fibonacci(22)`, the encoded data should be:

```
0x0000000000000000000000000000000000000000000000000000000000000016
```

To simulate contract testing and pass this data to the ABCI Core, run:

```sh
INIT_DATA=0x0000000000000000000000000000000000000000000000000000000000000016 npm run app
```

#### 3️⃣ Expected Output

Once the ABCI Core completes execution, the computed result will be settled back into the smart contract.

For `fibonacci(22)`, we expect the following results:

```
fib(22) result: 17711  
Encoded result: 0x000000000000000000000000000000000000000000000000000000000000452f
```

The final encoded output:

```
0x000000000000000000000000000000000000000000000000000000000000452f
```

This value will be used in the settlement process when calling the **Outpost Smart Contract** in the next step.

