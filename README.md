# AI Supabase Stack - Self-Hosted AI Hub

**AI Supabase Stack** is a comprehensive, self-hosted Docker Compose template that provides a complete AI development and deployment environment. This stack combines multiple AI tools and services to create a powerful local AI hub for individuals and businesses.

This fully integrated solution provides everything you need to build, deploy, and manage AI workflows, chatbots, and intelligent applications entirely on your own infrastructure.

### What's included

✅ [**n8n**](https://n8n.io/) - Low-code workflow automation platform with over 400 integrations and advanced AI components

✅ [**Supabase**](https://supabase.com/) - Open-source Firebase alternative with real-time database, authentication, and APIs

✅ [**Ollama**](https://ollama.com/) - Local LLM platform for running the latest open-source language models

✅ [**Open WebUI**](https://openwebui.com/) - Modern ChatGPT-like interface for interacting with your local AI models

✅ [**Flowise**](https://flowiseai.com/) - Visual AI agent builder with drag-and-drop interface

✅ [**Qdrant**](https://qdrant.tech/) - High-performance vector database for semantic search and RAG applications

✅ [**PostgreSQL**](https://www.postgresql.org/) - Robust relational database for data storage and management

## Installation

### Prerequisites

- Docker and Docker Compose installed
- At least 8GB RAM recommended
- 20GB+ free disk space

### For Nvidia GPU users

```bash
git clone https://github.com/your-username/ai-supabase-stack.git
cd ai-supabase-stack
docker compose --profile gpu-nvidia up -d
```

> [!NOTE]
> If you haven't used your Nvidia GPU with Docker before, install the [NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html) first.

### For Mac / Apple Silicon users

```bash
git clone https://github.com/your-username/ai-supabase-stack.git
cd ai-supabase-stack
docker compose up -d
```

For better performance on Mac, consider running Ollama natively and connecting to it from the stack using `http://host.docker.internal:11434/`.

### For CPU-only systems

```bash
git clone https://github.com/your-username/ai-supabase-stack.git
cd ai-supabase-stack
docker compose --profile cpu up -d
```

## ⚡️ Quick Start Guide

After installation, follow these steps to get your AI hub running:

### 1. Access the Services

- **n8n Workflow Automation**: <http://localhost:5678/>
- **Open WebUI**: <http://localhost:3000/>
- **Flowise AI Builder**: <http://localhost:3001/>
- **Supabase Dashboard**: <http://localhost:8000/>
- **Qdrant Dashboard**: <http://localhost:6333/dashboard>

### 2. Initial Setup

1. **Set up n8n**: Visit <http://localhost:5678/> and create your local admin account
2. **Configure Supabase**: Visit <http://localhost:8000/> and set up your project
3. **Set up Open WebUI**: Visit <http://localhost:3000/> and create your local account
4. **Access Flowise**: Visit <http://localhost:3001/> to start building AI agents

### 3. Configure Connections

Create credentials in n8n for the included services:

- **Ollama**: `http://ollama:11434`
- **PostgreSQL**: Use credentials from `.env` file, host: `postgres`
- **Qdrant**: `http://qdrant:6333` (no API key needed for local setup)
- **Supabase**: Use your project URL and service key

### 4. Deploy Your First AI Model

1. Pull a model in Ollama: `docker exec -it ollama ollama pull llama3.1`
2. Test the model in Open WebUI
3. Create your first AI workflow in n8n
4. Build visual AI agents in Flowise

## 🔧 Configuration

### Environment Variables

Copy `.env.example` to `.env` and customize:

```bash
cp .env.example .env
```

Key variables:
- `POSTGRES_DB`, `POSTGRES_USER`, `POSTGRES_PASSWORD`
- `SUPABASE_JWT_SECRET`
- `SUPABASE_ANON_KEY`, `SUPABASE_SERVICE_ROLE_KEY`

### Data Persistence

All data is persisted in Docker volumes:
- `postgres_data`: Database storage
- `qdrant_data`: Vector database storage
- `n8n_data`: Workflow and credential storage
- `supabase_data`: Supabase configuration and data

## 🚀 Use Cases

### Personal AI Assistant
- Create custom chatbots with your documents
- Automate personal workflows
- Build RAG applications with your data

### Business Intelligence
- Process and analyze business documents
- Create automated reporting workflows
- Build customer service chatbots

### Development & Prototyping
- Rapid AI application development
- Test different LLM models locally
- Build and deploy AI APIs

## 📚 Getting Started Tutorials

### Building Your First RAG Application
1. Upload documents to the shared folder
2. Create an embedding workflow in n8n
3. Store vectors in Qdrant
4. Build a chat interface in Open WebUI

### Creating AI Workflows
1. Use n8n's AI nodes for text processing
2. Connect to your local Ollama models
3. Integrate with external APIs
4. Set up automated triggers

### Visual AI Agent Building
1. Use Flowise for drag-and-drop AI workflows
2. Connect multiple AI models in chains
3. Create conversational agents
4. Deploy agents via API endpoints

## 🔄 Upgrading

To update all services:

```bash
docker compose pull
docker compose down
docker compose up -d
```

For GPU users:
```bash
docker compose --profile gpu-nvidia pull
docker compose down
docker compose --profile gpu-nvidia up -d
```

## 🛠️ Troubleshooting

### Common Issues

**Services won't start**: Check Docker resources and ensure ports aren't in use
**Slow performance**: Increase Docker memory allocation or use GPU acceleration
**Connection errors**: Verify service names in credentials match Docker service names

### Logs

View logs for specific services:
```bash
docker compose logs [service-name]
```

## 📁 File System Access

The stack includes a shared volume mounted at `/data/shared` in the n8n container, allowing workflows to access local files. Place files you want to process in the `./shared` directory.

## 🔒 Security Notes

This stack is designed for local development and testing. For production use:
- Change default passwords
- Enable authentication on all services
- Use proper SSL certificates
- Configure firewall rules

## 📜 License

This project is open source and available under the MIT License. See the [LICENSE](LICENSE) file for details.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit issues and pull requests.

## 📞 Support

- Check the [Issues](../../issues) page for common problems
- Review individual service documentation
- Join the community discussions
interact with the local filesystem.

**Nodes that interact with the local filesystem**

- [Read/Write Files from Disk](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.filesreadwrite/)
- [Local File Trigger](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.localfiletrigger/)
- [Execute Command](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.executecommand/)

## 📜 License

This project (originally created by the n8n team, link at the top of the README) is licensed under the Apache License 2.0 - see the
[LICENSE](LICENSE) file for details.
