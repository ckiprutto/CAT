# Docker Containerization Assignment – Yolomy E-commerce Application

## 1. Base Images

The following base images were selected:

- node:20-alpine – Used to run the Node.js backend.
- node:20-alpine – Used as the frontend build environment.
- nginx:alpine – Serves the compiled React frontend.
- mongo:7 – Runs the MongoDB database.

Alpine images were selected because they are lightweight and help reduce image sizes.

## 2. Dockerfile Instructions

The Dockerfiles use the following instructions:

- FROM: Specifies the base image.
- WORKDIR: Sets the working directory inside the container.
- COPY: Copies application files into the image.
- RUN: Executes commands during image building.
- ENV: Sets environment variables.
- EXPOSE: Documents the port used by the application.
- CMD: Specifies the command used to start the container.

The frontend uses a multi-stage build. Node.js builds the React application, while Nginx serves the production files.

## 3. Docker Compose and Orchestration

Docker Compose manages three services:

1. Backend – Node.js and Express API.
2. Frontend – React application served by Nginx.
3. MongoDB – Database service.

The services are defined in docker-compose.yml and run together using:

    docker compose up -d

## 4. Networking and Ports

A custom bridge network named yolo_network connects the three services.

The backend communicates with MongoDB using:

    mongodb://mongo:27017/yolomy

Port mappings:

- Frontend: localhost:3000 maps to container port 80.
- Backend: localhost:5000 maps to container port 5000.
- MongoDB: localhost:27017 maps to container port 27017.

Docker Compose service names allow containers to communicate without using localhost.

## 5. Data Persistence

A named Docker volume called mongo_data stores MongoDB database files.

The volume is mounted at:

    /data/db

This ensures database records remain available when containers are stopped or recreated, provided the volume is not deleted.

## 6. Git Workflow

Git is used for version control, while GitHub hosts the remote repository.

The workflow involves:

- Cloning the repository.
- Creating and modifying project files.
- Staging changes using git add.
- Saving changes using git commit.
- Uploading changes using git push.

## 7. Docker Image Naming and Versioning

The published images use the following names:

- ckiprutto/yolo-backend:v1.0.0
- ckiprutto/yolo-frontend:v1.0.0

The v1.0.0 tag follows Semantic Versioning:

- Major version: 1
- Minor version: 0
- Patch version: 0

The images are published on Docker Hub and can be downloaded using docker pull.

## 8. Deployment

The application can be deployed using the published Docker images and Docker Compose.

To download the images:

    docker compose pull

To start the application:

    docker compose up -d

To check running containers:

    docker compose ps

To stop the application:

    docker compose down
