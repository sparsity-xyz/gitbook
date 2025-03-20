# Publish Docker

## **Publishing Your Docker Image for Sparsity’s Ephemeral Roll-Up Network**

To enable Sparsity to load and run your Docker image within the ephemeral roll-up network, follow these straightforward steps. If you're unfamiliar with **Docker**, you can get more details [here](https://docs.docker.com/get-started/).

### **Step 1: Build the Docker Image**

#### **1️⃣ Create a Dockerfile**

Ensure that your project directory includes a **Dockerfile**—this file outlines the instructions needed to build your Docker image. If you’re new to Dockerfiles, [this guide](https://docs.docker.com/engine/reference/builder/) will help you get started.

#### **2️⃣ Build the Docker Image**

Open a terminal, navigate to your project directory, and run the following command:

```bash
docker build --platform linux/amd64 -t <registry>/<repository>:<tag> .
```

* Replace `registry`, `repository`, and `tag` with your specific values.
* The **tag** is optional but recommended for versioning.

### **Step 2: Publish the Docker Image**

#### **1️⃣ Log in to Docker Hub**

If you haven't already, log in to your **Docker Hub** account by running:

```bash
docker login
```

You will be prompted to enter your **Docker Hub username** and **password**.

#### **2️⃣ Push the Image to Docker Hub**

Once the image is built, push it to **Docker Hub** with the following command:

```bash
docker push <registry>/<repository>:<tag>
```

This action will make your image publicly available for others to download and use.

### **Step 3: Allow Others to Download the Image**

#### **1️⃣ Share the Image Name**

Provide others with your image name and tag, e.g.:

```
<registry>/<repository>:<tag>
```

#### **2️⃣ Pull the Image**

Others can download your Docker image by running:

```bash
docker pull <registry>/<repository>:<tag>
```

#### **3️⃣ Run the Image**

After the image has been pulled, users can verify that it is running correctly by executing:

```bash
docker run -d <registry>/<repository>:<tag>
```

***

With your Docker image successfully published, it can now be integrated into **Sparsity’s ephemeral roll-up network**, enabling efficient and scalable decentralized computation. 🚀

#### **Notes**:

For more information on how to run containers, check out [Docker's official documentation](https://docs.docker.com/get-started/overview/).
