# First DApp Setup Guide

This guide walks you through setting up and running the Fibonacci DApp on your local machine using Docker and Sparsity services.

***

### 1. Clone the Repository

First, pull the project from GitHub and navigate to the correct directory:

```sh
git clone https://github.com/sparsity-xyz/demo.git
cd demo/fibonacci-js
```

***

### 2. Build the Docker Image

The Docker image contains the **ABCI core**, encapsulating all computation and execution logic.

```sh
cd server
docker build -t abci-fib:latest .
```

***

### 3. Start the Chain Node & Deploy the Smart Contract

This step simulates a local EVM-based blockchain and deploys the Fibonacci smart contract.

```sh
cd contract
npm install
cp .env.example .env
make node
```

Wait until blocks start building before proceeding. Check the terminal output to ensure blocks are being produced.

***

### 4. Start the Bridge

The **Bridge service** connects the local EVM chain with the Sparsity platform.

#### Pull the Bridge Image

```sh
docker pull sparsityxyz/bridge:latest
```

#### Run the Bridge

*   **macOS:**

    ```sh
    docker run --rm -ti -e HOST=host.docker.internal sparsityxyz/bridge:latest
    ```
*   **Linux:**

    ```sh
    docker run --rm -ti -e HOST=172.17.0.1 sparsityxyz/bridge:latest
    ```

***

### 5. Start the Fleet

The **Fleet service** is responsible for triggering the Sparsity execution session when receiving signals from the Bridge.

#### Pull the Fleet Image

```sh
docker pull sparsityxyz/fleet:latest
```

#### Initialize Fleet

*   **macOS:**

    ```sh
    docker run -ti --rm \
        -v ./.data:/root/.fleet \
        -v /var/run/docker.sock:/var/run/docker.sock \
        sparsityxyz/fleet:latest fleet init --local
    ```
*   **Linux:**

    ```sh
    docker run -ti --rm \
        -v ./.data:/root/.fleet \
        -v /var/run/docker.sock:/var/run/docker.sock \
        --add-host=host.docker.internal:172.17.0.1 \
        sparsityxyz/fleet:latest fleet init --local
    ```

#### Register Fleet

*   **macOS:**

    ```sh
    docker run -ti --rm \
        -v ./.data:/root/.fleet \
        -v /var/run/docker.sock:/var/run/docker.sock \
        sparsityxyz/fleet:latest fleet register --ip 127.0.0.1
    ```
*   **Linux:**

    ```sh
    docker run -ti --rm \
        -v ./.data:/root/.fleet \
        -v /var/run/docker.sock:/var/run/docker.sock \
        --add-host=host.docker.internal:172.17.0.1 \
        sparsityxyz/fleet:latest fleet register --ip 127.0.0.1
    ```

#### Run Fleet

*   **macOS:**

    ```sh
    docker run -ti --rm \
        -v ./.data:/root/.fleet \
        -v /var/run/docker.sock:/var/run/docker.sock \
        sparsityxyz/fleet:latest fleet run
    ```
*   **Linux:**

    ```sh
    docker run -ti --rm \
        -v ./.data:/root/.fleet \
        -v /var/run/docker.sock:/var/run/docker.sock \
        --add-host=host.docker.internal:172.17.0.1 \
        sparsityxyz/fleet:latest fleet run
    ```

***

### 🎉 Your Fibonacci DApp is Now Running

At this point, your **end-to-end Fibonacci DApp** is successfully running on your local machine, integrated with the Sparsity platform. 🚀

