# Implementation of Reverse Proxy with Docker

# Project Overview

This project involves creating a simple development environment using React (JavaScript) and Flask (Python). By using Nginx as a reverse proxy, when users access `http://localhost`, they see a button labeled 'Osaka' on the front end built with React. Clicking this button triggers a response from the Flask-powered backend, saying "USJ is famous," which is then displayed on the front end.


## Technology Stack

- Frontend: React (JavaScript)
- Backend: Flask (Python)
- Reverse Proxy: Nginx
- Container Orchestration: Docker Compose

## Features

- Integration of frontend and backend on localhost
- Display of backend response upon button click
- Configuration of reverse proxy using Nginx

## Directory Structure

- `backend/`: Directory containing the Flask application. Includes Dockerfile, [app.py](http://app.py/), and requirements.txt.
- `frontend/`: Directory containing the React application. Includes the build folder, node_modules, public/index.html, src folder, Dockerfile, package-lock.json, and package.json.
- `nginx/`: Directory containing Nginx configuration file default.conf.
- `docker-compose.yml`: Configurations for launching services using Docker Compose.

![例の画像](https://github.com/KeishiNishio/reverse_proxy_with_Docker/blob/main/systemimage.png)


## Setup Instructions

1. Create Docker network:
    
    ```bash
    docker network create nginx-network
    ```
    
2. Install dependencies for the frontend
    
    ```bash
    cd frontend
    npm install
    export NODE_OPTIONS=--openssl-legacy-provider
    npm run build
    cd ..
    ```
    
3. Build and launch services using Docker Compose:
    
    ```bash
    docker-compose build --no-cache
    docker-compose up -d
    ```
    

## Other Useful Commands

- Commands for Docker cache deletion, network inspection, container status check, etc.
1. Delete all Docker cache system-wide

```bash
docker system prune --all --force
```

2. Check if containers are connected to the configured network

```bash
docker network inspect nginx-network
```

3. Check the status of containers

```bash
docker ps -a
```

4. Stop all existing containers

```bash
docker stop $(docker ps -aq) || true
```

5. Remove all existing containers

```bash
docker rm -f $(docker ps -aq) || true
```

## Development Environment

This project is developed in the following environment:

- **Operating System**: macOS
- **Docker**:
  - Version: 24.0.5
- **Docker Compose**:
  - Version: 2.23.3

## References

[Building a Simple Development Environment Using Docker, React, Python, and FastAPI with Reverse Proxy](https://cloudsmith.co.jp/blog/virtualhost/docker/2022/12/2241971.html)
