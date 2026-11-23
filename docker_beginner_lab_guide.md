# Docker Beginner Lab: Step-by-Step Workflow Guide

This document outlines the fundamental workflow for managing Docker images, creating and running containers, mapping network ports, inspecting logs, and executing containers in detached mode.

---

## Section 1: Image Management (Pulling, Listing & Removing)
In this first phase, we inspect local Docker images, download specific image versions (tags) from Docker Hub, and clean up unused images.

| Step | Action / Description | Commands | Screenshot |
| :--- | :--- | :--- | :--- |
| **1.1** | List currently available local images, download the default `node` image (`latest`), and verify the download. | `docker images`<br>`docker pull node`<br>`docker images` | *[Insert Screenshot 1.1 here]* |
| **1.2** | Pull a specific version tag (`node:18`) and the `mysql` image (Docker automatically converts image names to lowercase), then list all images. | `docker pull node:18`<br>`docker pull mysql`<br>`docker images` | *[Insert Screenshot 1.2 here]* |
| **1.3** | Remove the downloaded `node` and `mysql` images from local storage and verify that the list is clean. | `docker image rm node:18`<br>`docker images`<br>`docker image rm node:latest`<br>`docker image rm mysql:latest`<br>`docker images` | *[Insert Screenshot 1.3 here]* |

---

## Section 2: Basic Container Lifecycle (Create, Start, Stop & Remove)
Here, we download the `mongo` image and learn how to manually create, start, inspect, stop, and delete a container using its auto-generated ID.

| Step | Action / Description | Commands | Screenshot |
| :--- | :--- | :--- | :--- |
| **2.1** | Pull the `mongo` image and create a new container instance (this generates a unique container ID without starting it yet). | `docker pull mongo`<br>`docker create mongo` | *[Insert Screenshot 2.1 here]* |
| **2.2** | Start the container using its full ID and check running containers with `docker ps`. | `docker start 3284cd0bddc36f442b9c0a0835adf397776e9a9f17626f73a0474e288823c194`<br>`docker ps` | *[Insert Screenshot 2.2 here]* |
| **2.3** | Stop the running container using its short ID, check running containers (`ps`), and view all containers including stopped ones (`ps -a`). | `docker stop 3284cd0bddc3`<br>`docker ps`<br>`docker ps -a` | *[Insert Screenshot 2.3 here]* |
| **2.4** | Permanently remove the stopped container and verify that no containers remain in the system. | `docker rm 3284cd0bddc3`<br>`docker ps -a` | *[Insert Screenshot 2.4 here]* |

---

## Section 3: Named Containers & Port Mapping
Working with random container IDs is inconvenient. In this section, we assign custom names (`--name`) and expose container ports (`-p`) to make services accessible from the host machine.

| Step | Action / Description | Commands | Screenshot |
| :--- | :--- | :--- | :--- |
| **3.1** | Create and start a named container (`monguito`), verify it is running, and observe what happens when trying to remove a running container without stopping it first (or remove it after stopping). | `docker create --name monguito mongo`<br>`docker start monguito`<br>`docker ps`<br>`docker stop monguito`<br>`docker rm monguito` | *[Insert Screenshot 3.1 here]* |
| **3.2** | Create and start `monguito` again, mapping host port `27017` to container port `27017` (`-p 27017:27017`). | `docker create -p 27017:27017 --name monguito mongo`<br>`docker start monguito`<br>`docker ps` | *[Insert Screenshot 3.2 here]* |
| **3.3** | Create a second container (`monguito2`) using dynamic host port assignment (`-p 27017`), verify the assigned port in `docker ps`, then stop and remove `monguito2`. | `docker create -p 27017 --name monguito2 mongo`<br>`docker start monguito2`<br>`docker ps`<br>`docker stop monguito2`<br>`docker rm monguito2` | *[Insert Screenshot 3.3 here]* |

---

## Section 4: Inspecting Logs & Full Cleanup
Logs allow us to monitor what is happening inside a running container. Afterward, we stop and delete the container along with its base image.

| Step | Action / Description | Commands | Screenshot |
| :--- | :--- | :--- | :--- |
| **4.1** | View static logs from `monguito` and stream real-time logs using the `--follow` flag (press `Ctrl + C` to exit the stream). | `docker logs monguito`<br>`docker logs --follow monguito` | *[Insert Screenshot 4.1 here]* |
| **4.2** | Stop and remove `monguito`, then delete the local `mongo` image and verify that the image list is empty. | `docker stop monguito`<br>`docker rm monguito`<br>`docker image rm mongo`<br>`docker images` | *[Insert Screenshot 4.2 here]* |

---

## Section 5: Running Containers (`docker run`) & Detached Mode (`-d`)
The `docker run` command combines `pull`, `create`, and `start` into a single step. Here, we compare foreground execution against background (detached) execution.

| Step | Action / Description | Commands | Screenshot |
| :--- | :--- | :--- | :--- |
| **5.1** | Run `mongo` in the foreground (it automatically pulls the image), stop it with `Ctrl + C`, check container statuses, and clean up the container and image. | `docker run mongo`<br>*(Press `Ctrl + C` to stop)*<br>`docker ps`<br>`docker ps -a`<br>`docker rm 34ec2468c3f3`<br>`docker image rm mongo` | *[Insert Screenshot 5.1 here]* |
| **5.2** | Run `mongo` in detached/background mode (`-d`), check running containers, then stop and remove it using its container ID. | `docker run -d mongo`<br>`docker ps`<br>`docker stop 8cb681574e9a`<br>`docker rm 8cb681574e9a` | *[Insert Screenshot 5.2 here]* |
| **5.3** | Launch a production-style container in a single command: named `monguito`, mapping host port `29017` to container port `27017`, running in detached mode (`-d`), and verify its status. | `docker run --name monguito -p 29017:27017 -d mongo`<br>`docker ps` | *[Insert Screenshot 5.3 here]* |