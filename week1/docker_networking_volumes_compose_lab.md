# Docker Intermediate Lab: Networks, Custom Images, Volumes & Compose

This document covers a complete multi-container workflow using a Node.js (`Express` + `Mongoose`) application connected to a `MongoDB` database. It transitions from manual container networking to automated orchestration using **Docker Compose**, persistent volumes, and live-reloading development environments.

---

## Project Architecture Overview
Before starting, our base repository (`mongoapp-docker-p1`) contains a simple Node.js REST API (`index.js`) with two endpoints (`/` to list records and `/crear` to insert a record) that connects to a MongoDB host named `monguito` using credentials (`alan:password`).

* **`Dockerfile` & `docker-compose.yml`**: Used for standard/production-like builds.
* **`Dockerfile.dev` & `docker-compose-dev.yml`**: Used for local development with **nodemon** and **bind mounts** so code changes apply immediately without rebuilding the image.

---

## Section 1: Docker Network Management
Containers are isolated by default. To allow our Node.js app container (`chanchito`) to communicate with the MongoDB container (`monguito`) by its container name, we must create a custom bridge network.

| Step | Action / Description | Commands | Screenshot |
| :--- | :--- | :--- | :--- |
| **1.1** | Inspect existing local images and list all available Docker networks (`bridge`, `host`, `none`). | `docker images`<br>`docker network ls` | *[Insert Screenshot 1.1 here]* |
| **1.2** | Practice creating and removing a custom network named `mired` to understand network lifecycle management. | `docker network create mired`<br>`docker network ls`<br>`docker network rm mired`<br>`docker network ls` | *[Insert Screenshot 1.2 here]* |
| **1.3** | Navigate into the project folder (`mongoapp-docker-p1`) and create the final `mired` network that our containers will share. | `cd .\mongoapp-docker-p1\`<br>`docker network create mired` | *[Insert Screenshot 1.3 here]* |

---

## Section 2: Building a Custom Image & Manual Multi-Container Setup
In this section, we write our `Dockerfile` to package the Node.js application, build a custom image (`miapp:1`), and manually connect both containers inside `mired`.

### Reference: `Dockerfile` (Production)
```dockerfile
FROM node:latest
WORKDIR /home/app
COPY package*.json ./
RUN npm ci
COPY . .
EXPOSE 3000
CMD ["node", "index.js"]
```

| Step | Action / Description | Commands | Screenshot |
| :--- | :--- | :--- | :--- |
| **2.1** | Create the `Dockerfile` and build the custom image tagged as `miapp:1` from the current directory (`.`), then verify the image exists. | `docker build -t miapp:1 .`<br>`docker images` | *[Insert Screenshot 2.1 here]* |
| **2.2** | Check for any previous `monguito` container and remove it to avoid naming conflicts. | `docker ps -a`<br>`docker stop monguito`<br>`docker rm monguito` | *[Insert Screenshot 2.2 here]* |
| **2.3** | Create the `monguito` database container attached to `mired`, setting root credentials via environment variables (`-e`). | `docker create -p27017:27017 --name monguito --network mired -e MONGO_INITDB_ROOT_USERNAME=alan -e MONGO_INITDB_ROOT_PASSWORD=password mongo` | *[Insert Screenshot 2.3 here]* |
| **2.4** | Create the `chanchito` app container using `miapp:1` on the same `mired` network, then start both containers and verify their status. | `docker create -p3000:3000 --name chanchito --network mired miapp:1`<br>`docker ps -a`<br>`docker start monguito`<br>`docker start chanchito` | *[Insert Screenshot 2.4 here]* |

---

## Section 3: Simple Orchestration & Persistent Volumes (`docker-compose.yml`)
Instead of running long manual commands, **Docker Compose** defines all services, networks, ports, and volumes in a single YAML file.

### Key Concepts in `docker-compose.yml`
1. **Service Orchestration (`services`)**: Automatically creates a shared default network and links `chanchito` to `monguito`.
2. **Named Volumes (`monguito_data:/data/db`)**: Ensures that database records survive even if the `monguito` container is stopped or deleted. Docker manages this storage location on the host.

### Reference: `docker-compose.yml`
```yaml
services:
  chanchito:
    build: .
    ports:
      - "3000:3000"
    links:
      - monguito
  monguito:
    image: mongo:latest
    ports:
      - "27018:27017"
    environment:
      MONGO_INITDB_ROOT_USERNAME: alan
      MONGO_INITDB_ROOT_PASSWORD: password
    volumes:
      - monguito_data:/data/db

volumes:
  monguito_data:
```

| Step | Action / Description | Commands | Screenshot |
| :--- | :--- | :--- | :--- |
| **3.1** | Check the installed Docker Compose version and create the `docker-compose.yml` file in the root directory. | `docker --version`<br>*(Create `docker-compose.yml` in VS Code)* | *[Insert Screenshot 3.1 here]* |
| **3.2** | Build the images, create the named volume (`monguito_data`), and start both containers simultaneously using `docker compose up`. | `docker compose up` | *[Insert Screenshot 3.2 here]* |
| **3.3** | Inspect the generated images/containers and then tear down the environment cleanly with `docker compose down` (note: named volumes persist by default). | `docker images`<br>`docker ps -a`<br>`docker compose down` | *[Insert Screenshot 3.3 here]* |

---

## Section 4: Development Environment with Live-Reload & Volumes (`docker-compose-dev.yml`)
During development, rebuilding the image on every code edit is slow. We solve this using `Dockerfile.dev` (which installs `nodemon`) and **development volumes** in `docker-compose-dev.yml`.

### Key Concepts in `docker-compose-dev.yml`
1. **Bind Mount Volume (`.:/home/app`)**: Mirrors your local project folder directly inside the container's `/home/app` directory in real time. When you save `index.js`, `nodemon` inside the container detects the change and restarts the server automatically.
2. **Anonymous/Named Dependency Volume (`node_modules:/home/app/node_modules`)**: Prevents your local host folder from overwriting the container's compiled `node_modules` directory.

### Reference: `Dockerfile.dev` & `docker-compose-dev.yml`
```dockerfile
# Dockerfile.dev
FROM node:latest
WORKDIR /home/app
COPY package*.json ./
RUN npm ci
RUN npm install --global nodemon
COPY . .
EXPOSE 3000
CMD ["nodemon", "index.js"]
```

```yaml
# docker-compose-dev.yml
services:
  chanchito:
    build:
      context: .
      dockerfile: Dockerfile.dev
    ports:
      - "3000:3000"
    links:
      - monguito
    volumes:
      - .:/home/app
      - node_modules:/home/app/node_modules
  monguito:
    image: mongo:latest
    ports:
      - "27018:27017"
    environment:
      MONGO_INITDB_ROOT_USERNAME: alan
      MONGO_INITDB_ROOT_PASSWORD: password
    volumes:
      - monguito_data:/data/db

volumes:
  monguito_data:
  node_modules:
```

| Step | Action / Description | Commands | Screenshot |
| :--- | :--- | :--- | :--- |
| **4.1** | Create `Dockerfile.dev` (adding global `nodemon`) and `docker-compose-dev.yml` (configuring bind mounts and volumes). | *(Create `Dockerfile.dev` and `docker-compose-dev.yml` in VS Code)* | *[Insert Screenshot 4.1 here]* |
| **4.2** | Start the development stack by specifying the custom compose file with the `-f` flag. Test live-reloading by editing `index.js`. | `docker compose -f docker-compose-dev.yml up` | *[Insert Screenshot 4.2 here]* |