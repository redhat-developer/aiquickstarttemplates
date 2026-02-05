# Red Hat AI Quickstart Templates for Developer Hub

This repository contains Backstage/Red Hat Developer Hub templates for deploying Red Hat AI Quickstarts. These templates enable teams to quickly scaffold and deploy AI-powered applications on Red Hat OpenShift AI.

## Overview

Red Hat AI Quickstarts are ready-to-run, industry-specific use cases designed to demonstrate how Red Hat AI products can power real-world solutions on enterprise-ready, open source infrastructure.

## Available Templates

### 1. Generic AI Quickstart Template
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

### 2. IT Self-Service Agent
**Template ID:** `redhat-ai-it-self-service-agent`

Deploy an AI-powered self-service agent for IT process automation using agentic AI patterns.

**Features:**
- Llama 3 70B integration with LangGraph
- Testing mode (mock eventing) and production mode (Kafka + Knative)
- Safety guardrails (Llama Guard 3, PromptGuard)
- Multi-channel support (Slack, ServiceNow, CLI, Email)
- OpenTelemetry distributed tracing
- DeepEval framework for testing

**Technologies:**
- LangGraph (multi-step prompting)
- Llama 3 70B
- Kafka & Knative Eventing
- OpenTelemetry
- Model Context Protocol (MCP)

**Documentation:** [AI quickstart: Self-service agent for IT process automation](https://developers.redhat.com/articles/2026/01/26/ai-quickstart-self-service-agent-it-process-automation)

**Deployment Time:** 60-90 minutes (testing), 2-3 hours (production)

---

### 3. Product Recommender System
**Template ID:** `redhat-ai-product-recommender`

Build an AI-driven product recommendation system with semantic search and automated review summarization.

**Features:**
- Multiple ML model integration (embeddings, LLM, recommender)
- Feast feature store for data consistency
- KFP/Argo Workflows for ML pipelines
- KServe for model serving
- S3-compatible storage integration
- Jupyter notebooks for model development

**Technologies:**
- BAAI/BGE embeddings for text
- OpenAI/CLIP for images
- Llama 3.1 8B for summaries
- Two-tower recommender model
- Feast feature store
- OpenShift AI

**Documentation:** [AI quickstart: Product recommender with OpenShift AI](https://developers.redhat.com/articles/2026/01/20/ai-quickstart-product-recommender-openshift-ai)

---

### 4. Enterprise RAG Chatbot
**Template ID:** `redhat-ai-enterprise-rag-chatbot`

Deploy a Retrieval-Augmented Generation chatbot enhanced with company-specific data stores.

**Features:**
- Multiple vector database options (Milvus, pgvector, Redis, Qdrant)
- Configurable LLM providers (OpenShift AI, external APIs)
- Multiple data source connectors (Confluence, SharePoint, Google Drive)
- Automatic data synchronization
- Document chunking and embedding pipeline
- Customizable retrieval strategies

**Technologies:**
- Vector databases (Milvus recommended)
- Llama 3.1 or Mistral models
- BAAI/BGE embeddings
- Multiple data source integrations

**Use Cases:**
- Internal knowledge base chatbots
- Customer support automation
- Document Q&A systems
- Research assistance

---

### 5. LLM CPU Serving
**Template ID:** `redhat-ai-llm-cpu-serving`

Lightweight AI assistant serving small language models on CPU infrastructure.

**Features:**
- Multiple model sizes (1B, 3B, 7B parameters)
- CPU-optimized inference
- INT4/INT8 quantization support
- Response caching
- API authentication and rate limiting
- HuggingFace or custom model support

**Technologies:**
- TinyLlama, small Llama models
- CPU-optimized inference engines
- Model quantization
- OpenShift Routes

**Resource Requirements:**
- Small (1B): 2 CPU cores, 4GB RAM
- Medium (3B): 4 CPU cores, 8GB RAM
- Large (7B): 8 CPU cores, 16GB RAM

**Use Cases:**
- Cost-effective AI deployments
- Edge computing scenarios
- Development and testing
- Low-traffic AI services

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

### Example 1: Deploy LLM CPU Serving

```bash
# Simplest quickstart - no GPU required
# Model: TinyLlama 1.1B
# Resources: 2 CPU, 4GB RAM
# Time: 5 minutes
```

See [examples/llm-cpu-example-values.yaml](examples/llm-cpu-example-values.yaml)

### Example 2: Deploy IT Self-Service Agent

```bash
# Agentic AI for IT automation
# Requires: Llama 3 70B endpoint
# Integrations: Slack, ServiceNow
# Time: 60-90 minutes
```

See [examples/it-agent-example-values.yaml](examples/it-agent-example-values.yaml)

### Example 3: Deploy Enterprise RAG Chatbot

```bash
# RAG chatbot with vector database
# Vector DB: Milvus
# Data sources: Confluence, SharePoint
# Time: 20 minutes
```

See [examples/rag-chatbot-example-values.yaml](examples/rag-chatbot-example-values.yaml)

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

Based on Red Hat AI Quickstarts:
- IT Self-Service Agent: https://github.com/rh-ai-quickstart/it-self-service-agent
- LLM CPU Serving: https://github.com/rh-ai-quickstart/llm-cpu-serving
- Red Hat AI Services: https://github.com/redhat-ai-services

Built for Red Hat Developer Hub (Backstage).

---

## What's New

### Version 1.0.0 (2026-02-04)
- Initial release with 5 AI quickstart templates
- Generic template for flexibility
- IT Self-Service Agent with agentic AI
- Product Recommender with ML pipelines
- Enterprise RAG Chatbot with vector databases
- LLM CPU Serving for lightweight deployments
- Comprehensive documentation and examples
- Production-ready manifests with security best practices
