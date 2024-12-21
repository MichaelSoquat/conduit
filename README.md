# Conduit

## Table of Contents

- [Description](#description)
- [Quickstart](#quickstart)
- [Usage](#usage)
- [Dockerfiles](#dockerfiles)
- [docker-compose](#docker-compose)
- [docker-commands](#docker-commands) 
- [Automated-Workflow](#Automated-Workflow)

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
        docker compose up -d
        ```

> ⚠️ **Attention!**  
> Please adjust the environment files with the correct path to your server `<ip>/:<port>/api`.



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

https://github.com/MichaelSoquat/conduit/blob/main/docker-compose.yml

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

## Automated-Workflow

In the folder `.github` you see a workflow for automatically move the `.env` and the `docker compose` to the server https://github.com/MichaelSoquat/conduit/blob/main/.github/main.yml.
On top of that the frontend and the backend repo gets automatically moved to the server too.
It´s triggered with a push on the main branch.
Furthermore you can trigger the deploy process manually via github actions. It´s defined here: https://github.com/MichaelSoquat/conduit/blob/main/.github/deployment.yml.

Configuraiton of `secrets` and `variables` in github:

Go to the following path: `settings/security/Secrets and variables/actions`
- You have to define the following secrets

```
PAT	the personal access token	
TARGET_DIR	the target dir
SERVER_IP	the ip of your server
SSH_PRIVATE_KEY	the ssh private key to connect to server
USER	the username on the server
```

- And these are the variables:

```
API_URL	the backend url
DJANGO_SUPERUSER_USERNAME
DJANGO_SUPERUSER_PASSWORD
DJANGO_SUPERUSER_EMAIL
```

Notes:
If you don´t want to trigger the build you can create a new branch and do a PR on main branch.
To create and move to new branch you can use this code:

```
git checkout -b "new-branch-name"
```
 
