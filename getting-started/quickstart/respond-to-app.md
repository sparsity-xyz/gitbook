---
description: App Smart Contract Settlement
---

# Respond to App

## 3. Settling the Result to the App

With the settlement value obtained in the previous section, the **Outpost Contract** will use this value as input and write it back to the user-developed smart contract.

The result of `fibonacci(22)` must also be **ABI-encoded**. Retrieve the computed data from the **App ABCI Core** section and run the validation test:

#### 1️⃣ Navigate to the Contract Directory

```sh
cd contract
```

#### 2️⃣ Settle the Result

Run the following command to settle the computed result into the original smart contract:

```sh
RESULT=0x000000000000000000000000000000000000000000000000000000000000452f NUM=22 npx hardhat test test/app.ts --network localhost
```

Once executed, the result will be successfully recorded in the smart contract.

***

#### 🎉 Your Demo is Now Fully Set Up!

You have successfully completed the local setup for your demo. If you'd like to take it further, follow the **\[**[**deployment guide**](../../app-deployment/local.md)**]** to deploy Fibonacci as your first **Sparsity App**! 🚀
