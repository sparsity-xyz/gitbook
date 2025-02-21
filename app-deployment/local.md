# Deploy Smart Contract on Mainnet

## Contract Deployment Guide

Follow these steps to deploy your application to the Sparsity network in a production environment:

1.  Navigate to the contract directory:

    ```sh
    cd contract
    ```
2.  Copy the environment configuration for the Sepolia testnet:

    ```sh
    cp .env.example.sepolia .env
    ```
3. **Ensure you are targeting the correct outpost contract**. For example, our Base outpost contract can be found here:\
   [Base Sepolia Outpost Contract](https://sepolia.basescan.org/address/0x0E0F82D0253d81846d23Cf7e9562882222004731#code)
4.  Edit the `.env` file and add your deployer private key. Then, deploy the contract with cmd tool we provide in the [demo ](../getting-started/quickstart/)code base:

    ```sh
    make base-sepolia-deploy
    ```
5. If you need any assistance, contact our support team via Discord: [Join here](https://discord.com/invite/8bxcXmf3) for more details.

Once deployed, you should see the contract successfully live on **Base Sepolia**.
