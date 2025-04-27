# Self-hosted AI Domain Kit

**Self-hosted AI Domain Kit** is an open-source Docker Compose template designed to swiftly initialize a comprehensive local AI and low-code development environment with a custom domain and HTTPS.

Adapted from the [n8n Self-hosted AI Starter Kit](https://github.com/n8n-io/self-hosted-ai-starter-kit), it combines the self-hosted n8n platform with a curated list of compatible AI products and components to quickly get started with building self-hosted AI workflows.

## Getting Started: Setup Instructions

Follow these steps to set up your Self-hosted AI Domain Kit with a secure HTTPS connection:

### 1. Domain Registration

First, register a domain name from one of these popular registrars:

When selecting a domain, consider:
- Using a memorable, easy-to-type name
- Choosing a common TLD like .com for better recognition
- Ensuring it reflects your brand or purpose
- DNS setup
> To host n8n online or on a network, create a dedicated subdomain pointed at your server.
  - Add an A record to route the subdomain accordingly:
    - Type: A
    - Name: n8n (or the desired subdomain)
    - IP address: (your server's IP address)

### 2. Router Port Forwarding

To make your self-hosted system accessible from the internet:

1. Access your router's admin panel (typically at 192.168.0.1 or 192.168.1.1)
2. Navigate to the port forwarding section
3. Forward the following ports:
   - Port 80 (HTTP) → Your server's local IP address
   - Port 443 (HTTPS) → Your server's local IP address
4. Save the settings and restart your router if necessary

### 3. .env File Configuration

Create a `.env` file based on the provided `.env.example`:

1. Copy the `.env.example` file to `.env`
2. Configure these essential settings:
   ```
   DOMAIN_NAME=yourdomain
   SUBDOMAIN=n8n
   SSL_EMAIL=your-email@example.com
   
   # Security keys (use strong random strings)
   N8N_ENCRYPTION_KEY=your-long-random-string
   N8N_USER_MANAGEMENT_JWT_SECRET=another-long-random-string
   
   # Database credentials
   DB_TYPE=postgresdb
   DB_POSTGRESDB_HOST=postgres
   POSTGRES_USER=n8n
   POSTGRES_PASSWORD=your-strong-password
   POSTGRES_DB=n8n
   DB_POSTGRESDB_USER=${POSTGRES_USER}
   DB_POSTGRESDB_PASSWORD=${POSTGRES_PASSWORD}
   
   # Timezone
   GENERIC_TIMEZONE=UTC
   ```

### 4. Run Docker Compose

After setting up your folders and configuration:

```bash
# For Nvidia GPU users
docker compose --profile gpu-nvidia up

# For CPU-only systems
docker compose --profile cpu up
```

Your system will now be accessible at `https://n8n.yourdomain.com` (or whatever subdomain you configured).

## What's included

✅ **Self-hosted n8n** - Low-code platform with over 400 integrations and advanced AI components

✅ **Ollama** - Cross-platform LLM platform to install and run the latest local LLMs

✅ **Qdrant** - Open-source, high performance vector store with a comprehensive API

✅ **PostgreSQL** - Workhorse of the Data Engineering world, handles large amounts of data safely

✅ **Flowise** - Visual Langchain builder for creating and deploying AI workflows

✅ **Open WebUI** - Web interface for managing Ollama models and chat applications

## What you can build

⭐️ **AI Agents** for scheduling appointments

⭐️ **Summarize Company PDFs** securely without data leaks

⭐️ **Smarter Slack Bots** for enhanced company communications and IT operations

⭐️ **Private Financial Document Analysis** at minimal cost

## Folder Structure

The kit organizes files and directories as follows:

- **data/** - Main directory for all data-related files
  - **shared/** - Shared data accessible to n8n container
  - **videos/** - Storage for video files
  - **local-files/** - Local files accessible to services

- **n8n/backup/** - Backup and persistent storage for n8n
  - **credentials/** - Stored credentials for n8n workflows
  - **workflows/** - Saved n8n workflows
  - **.flowise/** - Flowise configuration
  - **open-webui/** - Open WebUI data
  - **postgresql/** - PostgreSQL database files
  - **n8n/** - n8n backup files
  - **qdrant/** - Qdrant vector database files

- **.cache/ollama/** - Cache directory for Ollama models

## Accessing local files

The shared folders are mounted to the n8n container to allow access to files on disk:
- Within the n8n container, the shared folder is located at `/data/shared`
- The local-files folder is mounted at `/files`

**Nodes that interact with the local filesystem:**
- Read/Write Files from Disk
- Local File Trigger
- Execute Command

## Networking

All services are connected to the `n8n_network` (named `self_hosted_ai_domain_kit`) for seamless communication.

## License

This project is licensed under the Apache License 2.0.
(Modified from https://github.com/n8n-io/self-hosted-ai-starter-kit)

## Support

For support and community discussions, visit the [n8n Forum](https://community.n8n.io/). 