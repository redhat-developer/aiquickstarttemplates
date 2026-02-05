# Red Hat AI Quickstart Templates for Developer Hub

This repository contains Backstage/Red Hat Developer Hub templates for deploying Red Hat AI Quickstarts. These templates enable teams to quickly scaffold and deploy AI-powered applications on Red Hat OpenShift AI.  



## Overview

Red Hat AI Quickstarts are ready-to-run, industry-specific use cases designed to demonstrate how Red Hat AI products can power real-world solutions on enterprise-ready, open source infrastructure.

** Please ensure that you validate and update these template for your enterprise use.  These are example templates and should not be used in production ***

## Available Templates

**All templates have 1:1 mapping with [rh-ai-quickstart](https://github.com/rh-ai-quickstart) repositories**

### 1. Enterprise RAG Chatbot ✅
**Template ID:** `redhat-ai-enterprise-rag-chatbot`
**Repository:** [rh-ai-quickstart/RAG](https://github.com/rh-ai-quickstart/RAG)

Deploy a Retrieval-Augmented Generation chatbot with company-specific data integration.

**Features:**
- Local (Podman/Ollama) and OpenShift (Helm/vLLM) deployment modes
- PGVector (PostgreSQL) for vector storage
- LlamaStack framework with Ollama
- Streamlit UI for chat interface
- Docling for advanced PDF processing
- Multiple data sources (GitHub, S3/MinIO, URLs)
- Llama 3.2-3B-Instruct or larger models
- all-MiniLM-L6-v2 embeddings
- Kubeflow Pipelines for ingestion (optional)

**Technologies:**
- Vector DB: PGVector (PostgreSQL)
- LLM: Llama 3.2 3B / 3.1 8B/70B
- Embedding: all-MiniLM-L6-v2
- Framework: LlamaStack
- UI: Streamlit
- Deployment: Podman Compose (local) or Helm (OpenShift)

**Hardware:** CPU/GPU (OpenShift), Intel Gaudi, NVIDIA GPU support

---

### 2. IT Self-Service Agent ✅
**Template ID:** `redhat-ai-it-self-service-agent`
**Repository:** [rh-ai-quickstart/it-self-service-agent](https://github.com/rh-ai-quickstart/it-self-service-agent)

Deploy an AI-powered self-service agent for IT process automation using agentic AI patterns.

**Features:**
- Llama 3 70B integration with LangGraph
- Testing mode (mock eventing) and production mode (Kafka + Knative)
- Safety guardrails (Llama Guard 3, PromptGuard)
- Multi-channel support (Slack, ServiceNow, CLI, Email)
- OpenTelemetry distributed tracing
- DeepEval framework for testing
- PostgreSQL for conversation state
- Request manager and specialist agent pattern

**Technologies:**
- LangGraph (multi-step prompting)
- Llama 3 70B
- Kafka & Knative Eventing
- OpenTelemetry
- Model Context Protocol (MCP)
- PostgreSQL

**Documentation:** [AI quickstart: Self-service agent for IT process automation](https://developers.redhat.com/articles/2026/01/26/ai-quickstart-self-service-agent-it-process-automation)

**Deployment Time:** 60-90 minutes (testing), 2-3 hours (production)

---

### 3. LLM CPU Serving - HR Assistant ✅
**Template ID:** `redhat-ai-llm-cpu-serving`
**Repository:** [rh-ai-quickstart/llm-cpu-serving](https://github.com/rh-ai-quickstart/llm-cpu-serving)

AI-powered HR Assistant using vLLM on CPU (no GPU required).

**Features:**
- TinyLlama 1.1B model optimized for CPU
- AnythingLLM workbench chat interface
- vLLM CPU runtime with OpenAI-compatible API
- Helm chart deployment on OpenShift AI
- Pre-configured "Assistant to the HR Representative" workspace
- Document-aware conversations with policy citations

**Technologies:**
- Model: TinyLlama 1.1B
- Runtime: vLLM CPU
- UI: AnythingLLM workbench
- Deployment: Helm
- Container: quay.io/rh-aiservices-bu/vllm-cpu-openai-ubi9

**Resource Requirements:**
- Minimum: 2 cores, 4GB RAM, 5GB storage
- Recommended: 8 cores, 8GB RAM (Intel AVX-512 preferred)

**Prerequisites:**
- OpenShift 4.16.24+
- OpenShift AI 2.16.2+
- Service Mesh & Serverless

**Use Case:** Financial services HR representatives seeking policy guidance

---

### 4. AI Virtual Agent Platform ✅
**Template ID:** `redhat-ai-virtual-agent`
**Repository:** [rh-ai-quickstart/ai-virtual-agent](https://github.com/rh-ai-quickstart/ai-virtual-agent)

Conversational AI agent platform with RAG, knowledge bases, and MCP server integration.

**Features:**
- React + PatternFly frontend UI
- FastAPI backend server
- LlamaStack AI platform (Ollama llama3.2:3b)
- PostgreSQL + pgvector for knowledge bases
- MinIO for file attachments
- Model Context Protocol (MCP) server
- Web search tool integration
- Safety guardrails and content filtering
- Agent management and configuration
- Streaming conversations with history
- Local (Docker Compose) and OpenShift deployment

**Technologies:**
- Frontend: React with PatternFly
- Backend: FastAPI
- AI: LlamaStack with Ollama
- Database: PostgreSQL + pgvector
- Storage: MinIO
- MCP: Model Context Protocol servers

**Prerequisites (OpenShift):**
- Cluster admin access for OAuth
- Red Hat OpenShift AI
- Hugging Face token (optional)

**Use Cases:** Customer service automation, IT support agents, knowledge base Q&A

---

### 5. AI Observability Summarizer ✅
**Template ID:** `redhat-ai-observability-summarizer`
**Repository:** [rh-ai-quickstart/ai-observability-summarizer](https://github.com/rh-ai-quickstart/ai-observability-summarizer)

Transform complex OpenShift AI metrics into actionable business insights.

**Features:**
- Natural language queries ("How is my GPU performing?")
- Multi-dashboard Streamlit interface (vLLM, OpenShift, Chat, GPU)
- AI-powered Slack alerts and notifications
- HTML/PDF/Markdown report generation
- Distributed tracing with Tempo
- Centralized logging with Loki
- OpenTelemetry Collector integration
- GPU & vLLM performance monitoring
- MCP server for Claude Desktop/Cursor
- Prometheus/Thanos metrics collection

**Technologies:**
- LLM: Llama 3.2 (1B/3B) or 3.1 (8B/70B)
- UI: Streamlit multi-dashboard
- Backend: Llama Stack
- Metrics: Prometheus/Thanos
- Tracing: Tempo + OpenTelemetry
- Logging: Loki
- Storage: MinIO

**Prerequisites:**
- OpenShift 4.16.24+
- OpenShift AI 2.16.2+
- Service Mesh & Serverless
- Prometheus/Thanos monitoring

**Use Cases:** AI operations monitoring, resource optimization, business ROI tracking

---

### 6. Generic AI Quickstart Template
**Template ID:** `redhat-ai-quickstart-generic`

A flexible template that can be adapted for any Red Hat AI quickstart with customizable parameters.

**Features:**
- Support for multiple quickstart repositories
- Configurable OpenShift deployment
- LLM model endpoint configuration
- Optional GitHub repository creation
- Kubernetes manifest generation

**Use Cases:**
- Experimenting with different AI quickstarts
- Quick prototyping
- Custom AI application deployments

---

## Quick Start

Get started in 5 minutes! See [QUICKSTART.md](QUICKSTART.md) for detailed instructions.

### 1. Register Templates in Developer Hub

Navigate to your Developer Hub instance and register this repository:

```
https://github.com/redhat-developer/aiquickstarttemplates/blob/main/catalog-info.yaml
```

### 2. Create Your First AI Quickstart

1. Go to **Create** in Developer Hub
2. Select **LLM CPU Serving** (easiest to start)
3. Fill in the form with your project details
4. Click **Create**

### 3. Deploy to OpenShift

```bash
# Clone the generated repository
git clone <your-generated-repo-url>
cd <project-name>

# Deploy to OpenShift
oc login --token=<token> --server=<cluster-url>
oc new-project <namespace>
oc apply -k manifests/
```

### 4. Test Your Deployment

```bash
# Get the route URL
export APP_URL=$(oc get route <app-name> -o jsonpath='{.spec.host}')

# Test the endpoint
curl https://$APP_URL/health
```

---

## Installation

### Prerequisites

1. **Red Hat Developer Hub** (Backstage) installed
2. **OpenShift Cluster** (4.17 or later recommended)
3. **OpenShift AI** operator installed
4. **GitHub** account for repository creation (optional)
5. **Git** client

### Step 1: Register Templates in Developer Hub

#### Option A: Direct Registration (Recommended)

1. Navigate to your Developer Hub instance
2. Go to **Create** → **Register Existing Component**
3. Enter the URL to this repository's `catalog-info.yaml`:
   ```
   https://github.com/redhat-developer/aiquickstarttemplates/blob/main/catalog-info.yaml
   ```
4. Click **Analyze** and then **Import**

#### Option B: App Config Registration

Add to your Developer Hub `app-config.yaml`:

```yaml
catalog:
  locations:
    - type: url
      target: https://github.com/redhat-developer/aiquickstarttemplates/blob/main/catalog-info.yaml
      rules:
        - allow: [Location, Template]
```

### Step 2: Configure Integrations (Optional)

For full functionality, configure these integrations in your `app-config.yaml`:

```yaml
integrations:
  github:
    - host: github.com
      token: ${GITHUB_TOKEN}

kubernetes:
  serviceLocatorMethod:
    type: 'multiTenant'
  clusterLocatorMethods:
    - type: 'config'
      clusters:
        - url: https://api.cluster.example.com:6443
          name: production
          authProvider: 'serviceAccount'
          skipTLSVerify: false
```

### Step 3: Set Up Secrets

Create a Kubernetes secret for sensitive credentials:

```bash
kubectl create secret generic ai-quickstart-credentials \
  --from-literal=github-token=<your-token> \
  --from-literal=llm-api-key=<your-key> \
  -n backstage
```

---

## Template Parameters

### Common Parameters (All Templates)

| Parameter | Description | Required | Default |
|-----------|-------------|----------|---------|
| `name` | Project name | Yes | - |
| `owner` | Team/user owner | Yes | - |
| `description` | Purpose description | No | - |
| `openshiftCluster` | OpenShift API URL | Yes | - |
| `namespace` | Target namespace | Yes | Template-specific |
| `createGitRepo` | Create GitHub repo | No | `true` |

### Template-Specific Parameters

See individual template documentation in the [templates](templates/) directory for complete parameter lists.

**Example configurations** are available in the [examples](examples/) directory.

---

## Architecture

### Template Structure

```
templates/
├── generic-ai-quickstart/
│   ├── template.yaml          # Template definition
│   └── skeleton/              # Template files
│       └── catalog-info.yaml  # Backstage catalog entry
├── it-self-service-agent/
│   └── template.yaml
├── product-recommender/
│   └── template.yaml
├── enterprise-rag-chatbot/
│   └── template.yaml
└── llm-cpu-serving/
    └── template.yaml
```

### Deployment Flow

1. **Template Selection:** User chooses template in Developer Hub
2. **Parameter Configuration:** User fills in required/optional parameters
3. **Scaffolding:** Template generates project structure
4. **Repository Creation:** (Optional) New GitHub repository created
5. **Manifest Generation:** Kubernetes manifests customized
6. **Catalog Registration:** Component registered in Backstage catalog
7. **Deployment:** User deploys to OpenShift using generated manifests

---

## Examples

### Example 1: Deploy Enterprise RAG Chatbot

```bash
# RAG chatbot with PGVector
# Local (Podman) or OpenShift (Helm)
# Data sources: GitHub, S3/MinIO, URLs
# Time: 10-15 minutes
```

See [examples/rag-chatbot-example-values.yaml](examples/rag-chatbot-example-values.yaml)

### Example 2: Deploy IT Self-Service Agent

```bash
# Agentic AI for IT automation
# Requires: Llama 3 70B endpoint
# Integrations: Slack, ServiceNow
# Time: 60-90 minutes
```

See [examples/it-agent-example-values.yaml](examples/it-agent-example-values.yaml)

### Example 3: Deploy LLM CPU Serving - HR Assistant

```bash
# HR Assistant on CPU - no GPU required
# Model: TinyLlama 1.1B with vLLM
# UI: AnythingLLM workbench
# Time: 5-10 minutes
```

See [examples/llm-cpu-example-values.yaml](examples/llm-cpu-example-values.yaml)

### Example 4: Deploy AI Virtual Agent

```bash
# Conversational AI platform
# React + FastAPI + LlamaStack
# Knowledge bases with RAG
# Time: 10-15 minutes
```

See [examples/ai-virtual-agent-example-values.yaml](examples/ai-virtual-agent-example-values.yaml)

### Example 5: Deploy AI Observability Summarizer

```bash
# AI-powered observability platform
# Streamlit multi-dashboard interface
# Natural language metrics queries
# Time: 10-15 minutes
```

See [examples/ai-observability-summarizer-example-values.yaml](examples/ai-observability-summarizer-example-values.yaml)

---

## Customization

### Creating Custom Templates

You can create custom templates by copying and modifying existing ones:

1. Copy a template directory:
   ```bash
   cp -r templates/generic-ai-quickstart templates/my-custom-template
   ```

2. Edit `template.yaml`:
   - Update `metadata.name` and `metadata.title`
   - Modify parameters as needed
   - Adjust steps for your workflow

3. Add to `catalog-info.yaml`:
   ```yaml
   targets:
     - ./templates/my-custom-template/template.yaml
   ```

### Modifying Existing Templates

To modify parameters or steps:

1. Edit the `template.yaml` file
2. Test locally using Backstage CLI:
   ```bash
   backstage-cli create --template ./templates/my-template/template.yaml
   ```
3. Commit and push changes
4. Templates will auto-update in Developer Hub

---

## Troubleshooting

### Template Not Appearing

**Problem:** Template doesn't show in Developer Hub catalog

**Solutions:**
- Verify `catalog-info.yaml` is accessible
- Check Developer Hub logs for parsing errors
- Ensure `kind: Template` is set correctly
- Refresh catalog: **Settings** → **Catalog** → **Refresh**

### GitHub Integration Issues

**Problem:** Cannot create GitHub repositories

**Solutions:**
- Verify `GITHUB_TOKEN` has `repo` scope
- Check token is configured in `app-config.yaml`
- Ensure `allowedHosts` includes `github.com`

### OpenShift Deployment Failures

**Problem:** Manifests fail to apply

**Solutions:**
- Verify OpenShift AI operators are installed
- Check namespace exists or create it
- Ensure service account has required permissions
- Review secret names match generated manifests

### Model Endpoint Issues

**Problem:** LLM endpoint not accessible

**Solutions:**
- Verify endpoint URL is correct
- Check API key is valid
- Ensure network policies allow egress
- Test endpoint manually: `curl -H "Authorization: Bearer $API_KEY" $ENDPOINT`

---

## Best Practices

### Security

1. **Never commit secrets** to templates or repositories
2. Use **Kubernetes Secrets** for sensitive data
3. Enable **RBAC** for namespace isolation
4. Use **private repositories** for production deployments
5. Enable **API authentication** for public endpoints

### Resource Management

1. Set appropriate **resource requests/limits**
2. Use **HPA (Horizontal Pod Autoscaler)** for production
3. Monitor **resource usage** with OpenShift monitoring
4. Consider **node affinity** for GPU/special hardware

### CI/CD Integration

1. Use **ArgoCD** or **Flux** for GitOps workflows
2. Implement **pre-commit hooks** for manifest validation
3. Set up **automated testing** for model endpoints
4. Use **staging environments** before production

### Cost Optimization

1. Use **CPU serving** for low-traffic workloads
2. Enable **model caching** to reduce inference costs
3. Implement **request batching** where applicable
4. Consider **spot instances** for training workloads

---

## Contributing

We welcome contributions to improve these templates!

### How to Contribute

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/my-improvement`
3. Make your changes
4. Test thoroughly
5. Submit a pull request

### Template Guidelines

- Follow existing template structure
- Include comprehensive parameter descriptions
- Add validation where appropriate
- Document all customization points
- Include example values

---

## Support

### Resources

- **Red Hat AI Quickstarts Documentation:** https://docs.redhat.com/en/learn/ai-quickstarts
- **Red Hat Developer Hub Documentation:** https://docs.redhat.com/en/documentation/red_hat_developer_hub
- **OpenShift AI Documentation:** https://docs.redhat.com/en/documentation/red_hat_openshift_ai
- **Backstage Documentation:** https://backstage.io/docs

### Community

- **Red Hat Developers:** https://developers.redhat.com
- **GitHub Issues:** https://github.com/redhat-developer/aiquickstarttemplates/issues
- **Red Hat Developer Forums:** https://developers.redhat.com/community

---

## License

This project is licensed under the Apache License 2.0 - see the LICENSE file for details.

---

## Acknowledgments

Based on official Red Hat AI Quickstarts (1:1 mapping):
- **Enterprise RAG:** https://github.com/rh-ai-quickstart/RAG
- **IT Self-Service Agent:** https://github.com/rh-ai-quickstart/it-self-service-agent
- **LLM CPU Serving:** https://github.com/rh-ai-quickstart/llm-cpu-serving
- **AI Virtual Agent:** https://github.com/rh-ai-quickstart/ai-virtual-agent
- **AI Observability Summarizer:** https://github.com/rh-ai-quickstart/ai-observability-summarizer
- **Red Hat AI Services:** https://github.com/redhat-ai-services

Built for Red Hat Developer Hub (Backstage).

All templates are verified against real rh-ai-quickstart repositories to ensure accuracy.

---

## What's New

### Version 2.0.0 (2026-02-04)
- ✅ **Verified 1:1 mapping** with real rh-ai-quickstart repositories
- ✅ Enterprise RAG Chatbot - Based on rh-ai-quickstart/RAG
- ✅ IT Self-Service Agent - Verified against real repo
- ✅ LLM CPU Serving - Updated to match HR Assistant implementation
- ✅ NEW: AI Virtual Agent - Conversational AI platform
- ✅ NEW: AI Observability Summarizer - AI-powered monitoring
- ✅ Generic template for flexibility
- All templates match actual quickstart implementations
- Updated documentation with features and prerequisites
- Example values for all 5 quickstarts

### Version 1.0.0 (2026-02-04)
- Initial release 
