# 🐳 Holberton School Softy Pinko Docker

## 📝 Description
This repository contains Docker exercises and projects for Holberton School's curriculum. It demonstrates the implementation of Docker containers and best practices for containerization.

## 🚀 Getting Started

### Prerequisites
- Docker installed on your system
- Docker Compose installed on your system
- Basic understanding of Docker concepts

### 🔧 Installation
1. Clone this repository:
```bash
git clone https://github.com/yourusername/holbertonschool-softy-pinko-docker.git
```

2. Navigate to the project directory:
```bash
cd holbertonschool-softy-pinko-docker
```

## 📁 Project Structure
- `task0/` - Basic Docker container setup
  - `Dockerfile` - Simple Ubuntu-based container that prints "Hello, World!"
- `task1/` - Python Flask API container
  - `Dockerfile` - Ubuntu-based container with Python3, pip3, and Flask
  - `api.py` - Simple Flask API that returns "Hello, World!" at the `/api/hello` endpoint
- `task2/` - Front-end and Back-end setup
  - `back-end/`
    - `Dockerfile` - Flask API container (from task1)
    - `api.py` - Flask API (from task1)
  - `front-end/`
    - `Dockerfile` - Nginx container to serve static front-end files
    - `softy-pinko-front-end/` - Cloned front-end application
    - `softy-pinko-front-end.conf` - Nginx configuration for the front-end
- `task3/` - Connecting Front-end and Back-end
  - (Structure similar to task2, with updates for CORS and front-end API calls)
- `task4/` - Docker Compose Setup
  - (Structure similar to task3)
  - `docker-compose.yml` - Docker Compose file to manage front-end and back-end services
- `task5/` - Proxy Server Setup
  - (Structure similar to task4, with an added proxy directory)
  - `proxy/`
    - `Dockerfile` - Nginx container for the proxy server
    - `proxy.conf` - Nginx configuration to route requests to front-end and back-end
  - `docker-compose.yml` - Updated to include the proxy service and manage all three services
- `task6/` - Horizontal Scaling
  - (Structure similar to task5)
  - `2-api-servers.txt` - Contains the command to scale the back-end service

## 🛠️ Usage

### Task 0: Basic Docker Container
```bash
# Build the Docker image
docker build -t softy-pinko-task0 ./task0

# Run the container
docker run softy-pinko-task0
```

### Task 1: Python Flask API
```bash
# Build the Docker image
docker build -t softy-pinko:task1 ./task1

# Run the container
docker run -p 5252:5252 -it --rm --name softy-pinko-task1 softy-pinko:task1
# Access API at http://localhost:5252/api/hello
```

### Task 2: Front-end and Back-end
```bash
# Build back-end
docker build -f ./task2/back-end/Dockerfile -t softy-pinko-back-end:task2 ./task2/back-end
# Run back-end
docker run -p 5252:5252 -d --name softy-pinko-back-end-task2 softy-pinko-back-end:task2

# Build front-end
docker build -f ./task2/front-end/Dockerfile -t softy-pinko-front-end:task2 ./task2/front-end
# Run front-end
docker run -p 9000:9000 -d --name softy-pinko-front-end-task2 softy-pinko-front-end:task2
# Access front-end at http://localhost:9000/softy-pinko-front-end/
```

### Task 3: Connecting Front-end and Back-end
(Similar build and run commands as Task 2, ensure you are in the `task3` directory or update paths accordingly)
```bash
# In terminal 1 (for back-end)
cd task3
docker build -f ./back-end/Dockerfile -t softy-pinko-back-end:task3 ./back-end
docker run -p 5252:5252 -it --rm --name softy-pinko-back-end-task3 softy-pinko-back-end:task3

# In terminal 2 (for front-end)
cd task3
docker build -f ./front-end/Dockerfile -t softy-pinko-front-end:task3 ./front-end
docker run -p 9000:9000 -it --rm --name softy-pinko-front-end-task3 softy-pinko-front-end:task3
# Access front-end at http://localhost:9000/softy-pinko-front-end/
```

### Task 4: Docker Compose
```bash
cd task4
docker-compose build
docker-compose up
# Access front-end at http://localhost:9000/softy-pinko-front-end/
# API accessible internally via http://back-end:5252/api/hello
```

### Task 5: Proxy Server
```bash
cd task5
docker-compose build
docker-compose up
# Access application via proxy at http://localhost/ (or http://localhost/softy-pinko-front-end/)
# API requests from front-end go to /api/hello, routed by proxy
```

### Task 6: Horizontal Scaling
```bash
cd task6
# Build images if not already built from task5 or if changes were made
docker-compose build 

# Run with scaled back-end (as per 2-api-servers.txt)
docker-compose up --scale back-end=2
# Access application via proxy at http://localhost/
```

## 📚 Learning Objectives
- Understanding Docker basics
- Creating and managing Docker containers
- Working with Dockerfiles
- Best practices for containerization
- Containerizing web applications and APIs
- Using Docker Compose for multi-container applications
- Implementing a reverse proxy with Nginx
- Horizontal scaling of services with Docker Compose

## 👤 Author
- Judith Espinal - Holberton Coding School Student