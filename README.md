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

  https://github.com/MichaelSoquat/conduit-frontend/blob/591c07be3b58aa589def6dc74df8b6361af8be38/Dockerfile

- **Backend-Dockerfile**:
  
 https://github.com/MichaelSoquat/conduit-backend/blob/e7c3d46d13dee30cb8e6be8b6923b266db97f161/Dockerfile

## docker-compose

https://github.com/MichaelSoquat/conduit/blob/main/docker-compose.yaml

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
 
