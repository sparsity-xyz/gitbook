# Prerequisites

First of all, ensure your system meets the following requirements:

#### Operating System

* macOS or Linux
* Windows users should use **WSL (Windows Subsystem for Linux)**

#### Dependencies

**1. Foundry**

[Foundry](https://book.getfoundry.sh/getting-started/installation) is a powerful smart contract development toolchain. Install it using:

```sh
curl -L https://foundry.paradigm.xyz | bash
foundryup
```

To verify installation:

```sh
forge --version
```

For detailed installation instructions, refer to the [official Foundry documentation](https://book.getfoundry.sh/getting-started/installation).

**2. Node.js & npm**

Ensure **Node.js** and **npm** are installed:

```sh
node -v
npm -v
```

If missing, install via:

*   **Using nvm (recommended):**

    ```sh
    curl -fsSL https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.4/install.sh | bash
    source ~/.bashrc  # or source ~/.zshrc
    nvm install --lts
    ```
*   **Using Homebrew (macOS):**

    ```sh
    brew install node
    ```

**3. Docker**

Docker is required for containerized execution. Install it via:

*   **macOS:**

    ```sh
    brew install --cask docker
    open /Applications/Docker.app
    ```
*   **Ubuntu/Linux:**

    ```sh
    sudo apt update
    sudo apt install -y docker.io
    sudo systemctl start docker
    sudo systemctl enable docker
    ```
* **Windows (via WSL):**
  1. Install [Docker Desktop](https://www.docker.com/products/docker-desktop/)
  2. Enable **WSL integration** in Docker settings

To verify installation, run:

```sh
docker --version
docker run hello-world
```
