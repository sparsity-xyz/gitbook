# Interact with the DApp

Now that everything is running locally, you can perform an **end-to-end test** by interacting with the deployed smart contract.

**📝 Compute Fibonacci for a Given Number**

To compute the Fibonacci sequence for a specific number (e.g., `10`), run:

```sh
make request-fib NUM=10
```

This command sends a request to the smart contract, triggering the computation process.

**⏳ Wait for Processing**

The **Bridge** and **Fleet** services will handle the request. Wait until the computation is completed before proceeding.

**📥 Retrieve the Result**

Once processed, fetch the computed Fibonacci result using:

```sh
make fib-result NUM=10
```

**✅ Expected Output**

```
55
```

This confirms that the computation was successfully executed using the Sparsity platform. 🎉
