# Deployment Plan: Headless Anki MCP Server

This document outlines the plan to deploy the headless Anki service and the Anki MCP server, and expose the MCP server for use with an existing Open Web UI installation.

## 1. Project Overview

The goal is to run a headless Anki instance with the AnkiConnect addon, and expose its functionality as an MCP server for Open Web UI.

The key components are:
- **`headless-anki-cloud`**: The main project directory located at `/home/joenathan/Desktop/Projects/Code/headless-anki-cloud`.
- **`Dockerfile`**: Located in the root directory, this file is used to build the headless Anki Docker image.
- **`anki-mcp`**: A submodule directory located at `headless-anki-cloud/anki-mcp` containing the MCP server, which is a Node.js application.
- **`data`**: A directory located at `headless-anki-cloud/data` containing the Anki user data.

## 2. The Plan

### Step 1: Create a Dockerfile for the Anki MCP Server

A `Dockerfile` will be created at `headless-anki-cloud/anki-mcp/Dockerfile` to containerize the MCP server.

**`anki-mcp/Dockerfile`:**
```dockerfile
FROM node:18-slim

WORKDIR /usr/src/app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 8080

CMD [ "npm", "start" ]
```

### Step 2: Parameterize the Anki MCP Server Configuration

The Anki MCP server will be modified to allow configuration through environment variables.

- **File to modify**: `headless-anki-cloud/anki-mcp/src/index.ts`
- **Change**: Modify the server to use the `PORT` environment variable to set the listening port.

- **File to modify**: `headless-anki-cloud/anki-mcp/src/utils.ts`
- **Change**: Modify the AnkiConnect URL to be configurable via the `ANKICONNECT_URL` environment variable.

### Step 3: Create a Docker Compose File

A `docker-compose.yml` file will be created in the root of the project (`/home/joenathan/Desktop/Projects/Code/headless-anki-cloud/docker-compose.yml`). This file will define and link the `anki` and `anki-mcp` services.

**`docker-compose.yml`:**
```yaml
version: '3.8'

services:
  anki:
    build:
      context: .
      dockerfile: Dockerfile
    volumes:
      - ./data:/root/.local/share/Anki2
    networks:
      - anki-net

  anki-mcp:
    build:
      context: ./anki-mcp
      dockerfile: Dockerfile
    ports:
      - "127.0.0.1:8081:8081" # Expose MCP server to the host
    environment:
      - PORT=8081
      - ANKICONNECT_URL=http://anki:8765
    depends_on:
      - anki
    networks:
      - anki-net

networks:
  anki-net:
```

### Step 4: Start the Services

The services will be started using the following command, executed from the root of the project:

```bash
docker-compose up --build -d
```

## 3. Expected Outcome

After executing the plan, the following will be true:
- The headless Anki service will be running in a Docker container.
- The Anki MCP server will be running in a Docker container.
- The Anki MCP server will be accessible from the host machine (the Oracle Cloud server) at `http://<your-server-ip>:8081`.
- You will be able to use this URL to configure the Anki MCP server in your Open Web UI installation.
