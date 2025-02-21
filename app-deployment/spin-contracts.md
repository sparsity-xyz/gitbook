# Register into Sparsity

## Register Your Application on the Sparsity Platform

To make your application available on the Sparsity platform, follow these steps:

**1. Build and Publish Your Application**

Your ABCI application must be packaged as a Docker image and pushed to a public registry.

* Build the Docker image and push it to your preferred registry (e.g., Docker Hub, AWS ECR, or GitHub Container Registry).
*   Retrieve the Docker image digest for verification using:

    ```sh
    docker images --digests
    ```
* Update your `.env` file with the following details:
  * `dockerURI`: The public URI of your Docker image
  * `dockerHash`: The digest hash of the image

**2. Register Your Contract with the Sparsity Outpost**

To enable interaction with the Sparsity network, register your contract with the Sparsity Outpost by running cmd tool provided in [demo ](broken-reference)code base:

```sh
make base-sepolia-register
```

