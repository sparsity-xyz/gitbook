# Verification

## Await Approval from Sparsity

Before your application becomes available on the Sparsity platform, it must undergo a review and approval process.

* Submit a request via our Discord: [Click here](https://discord.gg/PvS5yfPBwH).
* Wait for approval. You can track the status of your application through the Sparsity dashboard or other communication channels.

#### 1. Trigger the Application

Once approved, you can initiate computation by interacting with your deployed contract.

For example, if you deployed the demo **Fibonacci** application:

* Update `[APP_CONTRACT]` in your `.env` file.
*   Trigger the application by running:

    ```sh
    make base-sepolia-fib
    ```

#### 2. Retrieve and Verify the Result

Once the computation is complete, retrieve and verify the result, which is settled back into your contract, using:

```sh
make base-sepolia-fib-result
```
