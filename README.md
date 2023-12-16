# Custom PQC NGINX Server Project
 ** This is still testing and need improvement for test in web browser certificate and need to make it access with both classical and PQC.
## Introduction
This guide outlines the steps to install and use the Custom PQC NGINX Server in a Docker container. This project leverages Quantum-Safe cryptography with custom NGINX configurations to enhance security.

## Prerequisites
- **Docker**: Ensure Docker is installed on your system. If not, please download and install Docker from [Docker's official website](https://www.docker.com/get-started).

## Setup Instructions

1. **Create a Docker Network**:
   ```bash
   docker network create pqc-net
   ```

2. **Build the Custom PQC NGINX Docker Image**:
   ```bash
   docker build -t custom-pqc-nginx .
   ```

3. **Run the Docker Container**:
   ```bash
   docker run -d -p 4424:4433 --network pqc-net --name custom-pqc-nginx custom-pqc-nginx
   ```

4. **Inspect the Docker Container**:
   To find the IP address of the Docker container, run:
   ```bash
   sudo docker inspect custom-pqc-nginx | grep IPAddress
   ```
   The output should show the Docker project IP address under "IPAddress".

5. **Install Quantum-Safe Curl**:
   ```bash
   docker pull openquantumsafe/curl
   ```

6. **Run Quantum-Safe Curl in Docker**:
   ```bash
   docker run -it --network pqc-net openquantumsafe/curl sh
   ```

## Usage Examples

- **Without a Certificate or Using a Self-Signed Certificate**:
  - General request:
    ```bash
    curl -k https://{Docker_project_IP}:4433
    ```
  - Request with PQC KEM algorithms:
    ```bash
    curl -k --curve kyber768 https://{Docker_project_IP}:4433
    ```

- **With a Standard Certificate**:
  - General request:
    ```bash
    curl https://{Docker_project_IP}:4433
    ```
  - Request with PQC KEM algorithms:
    ```bash
    curl --curve kyber768 https://{Docker_project_IP}:4433
    ```

## Download
For the latest version of the Custom PQC NGINX Server Project, please visit the [download page](#).

