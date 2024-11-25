# Conduit

## Table of Contents

- [Description](#description)
- [Quickstart](#quickstart)
- [Usage](#usage)
- [Dockerfiles](#dockerfiles)
- [docker-compose](#docker-compose)
- [docker-commands](#docker-commands)

## Description

This repo has an angular frontend with a django backend splitted in submodules. Furthermore we have Docker compose, Dockerfiles, envs and entrypoints to dockerize the application.

## Quickstart

1. **Clone the repo and submodules:**
   ```bash
   git clone --recurse-submodules https://github.com/MichaelSoquat/conduit.git
   cd Conduit
   ```

2. **Init and update submodules:**
   ```bash
   git submodule update --init --recursive
   ```

3. **Create and set up .env:**
   
    ```
    DJANGO_SUPERUSER_EMAIL=admin@admin.com
    DJANGO_SUPERUSER_USERNAME=admin
    DJANGO_SUPERUSER_PASSWORD=admin
    ```

4. **Docker compose:**
        ```
        docker compose up
        ```

`Attention!`
Please adjust the environment files with the correct path to your server `<ip>/:<port>/api`


## Usage
After setting up the environment and starting the application, you can access the frontend and backend as follows:

- Frontend
Navigate to the frontend in your browser at: `http://<server-ip>:8282`
This will display the Angular-based UI, allowing you to interact with the application.
- Backend
The backend API is available at: `http://<server-ip>:8000/api`
You can use this endpoint to perform API requests, test endpoints, or integrate with other systems.


## Dockerfiles

- **Frontend-Dockerfile**:

  ```
  FROM node:20-alpine AS build

  WORKDIR /app
  
  COPY package.json package-lock.json ./
  
  RUN npm install
  
  COPY . .
  
  RUN npm run build --prod
  
  FROM nginx:alpine
  
  COPY --from=build /app/dist/* /usr/share/nginx/html
  
  EXPOSE 80
  ```

- **Backend-Dockerfile**:
  ```
  FROM python:3.6-slim as base
  
  RUN apt-get update \
      && apt-get install -y --no-install-recommends \
      gcc \
      python3-dev \
      musl-dev \
      libpq-dev \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

  WORKDIR /usr/src/app
  
  COPY requirements.txt .
  RUN pip install --no-cache-dir -r requirements.txt
  
  FROM base as build
  
  WORKDIR /usr/src/app
  
  COPY . .
  
  RUN chmod +x /usr/src/app/entrypoint.sh
  
  FROM python:3.6-slim
  
  COPY requirements.txt .
  RUN pip install --no-cache-dir -r requirements.txt
  
  WORKDIR /usr/src/app
  
  COPY --from=build /usr/src/app /usr/src/app
  
  EXPOSE 8000
  
  ENTRYPOINT ["/usr/src/app/entrypoint.sh"]
  ```

## docker-compose

```
services:
  backend:
    build:
      context: ./conduit-backend
      dockerfile: Dockerfile
    ports:
      - "8000:8000"
    env_file:
      - .env
    volumes:
      - conduit-db:/app/db_data
    restart: on-failure
  frontend:
    build:
      context: ./conduit-frontend
      dockerfile: Dockerfile
    ports:
      - "8282:80"
    restart: on-failure

    depends_on:
      - backend
volumes:
  conduit-db:
```

## docker-commands

- Stop a container:

```
docker stop <container_name_or_id>
```

- List all containers:

```
docker ps -a
```

- Remove a container:

```
docker rm <container_name_or_id>
```

- Logs from container:

```
docker logs <container_name_or_id>
```

- Access container shell:
```
docker exec -it <container_name_or_id> /bin/bash
```
 
