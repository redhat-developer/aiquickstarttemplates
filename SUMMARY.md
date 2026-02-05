# Red Hat AI Quickstart Templates - Project Summary

## What Was Built

This repository contains a complete set of Backstage/Red Hat Developer Hub templates for deploying Red Hat AI Quickstarts. The templates enable self-service deployment of AI-powered applications on Red Hat OpenShift AI.

## Repository Structure

```
aiquickstart/
├── catalog-info.yaml                    # Main catalog registration file
├── README.md                            # Comprehensive documentation
├── QUICKSTART.md                        # 5-minute getting started guide
├── .gitignore                           # Git ignore rules
├── examples/                            # Example parameter values
│   ├── it-agent-example-values.yaml
│   ├── product-recommender-example-values.yaml
│   ├── rag-chatbot-example-values.yaml
│   └── llm-cpu-example-values.yaml
└── templates/                           # Backstage templates
    ├── generic-ai-quickstart/           # Generic flexible template
    │   ├── template.yaml
    │   └── skeleton/
    │       └── catalog-info.yaml
    ├── it-self-service-agent/           # Agentic AI for IT automation
    │   └── template.yaml
    ├── product-recommender/             # ML-based recommender system
    │   └── template.yaml
    ├── enterprise-rag-chatbot/          # RAG chatbot with vector DB
    │   └── template.yaml
    └── llm-cpu-serving/                 # Lightweight CPU-based LLM
        └── template.yaml
```

## Templates Included

### 1. Generic AI Quickstart Template
**File:** `templates/generic-ai-quickstart/template.yaml`

A flexible, reusable template that can be adapted for any Red Hat AI quickstart. Includes:
- Configurable GitHub repository selection
- OpenShift deployment parameters
- LLM endpoint configuration
- Kubernetes manifest generation
- Optional GitHub repo creation

**Best for:** Quick experimentation and custom AI projects

---

### 2. IT Self-Service Agent
**File:** `templates/it-self-service-agent/template.yaml`

Comprehensive template for deploying agentic AI systems for IT process automation. Features:

**Parameters:**
- Deployment mode (testing with mock eventing or production with Kafka)
- Llama 3 70B model endpoint configuration
- Safety guardrails (Llama Guard 3, PromptGuard)
- Multi-channel integrations (Slack, ServiceNow, CLI, Email)
- OpenTelemetry distributed tracing

**Generated Artifacts:**
- Kustomize overlays for environment-specific config
- Kubernetes secrets for credentials
- ConfigMaps for agent configuration
- Optional ArgoCD Application manifest
- Catalog component registration

**Deployment Time:** 60-90 minutes (testing), 2-3 hours (production)

**Technologies:** LangGraph, Llama 3 70B, Kafka, Knative, OpenTelemetry, MCP

---

### 3. Product Recommender System
**File:** `templates/product-recommender/template.yaml`

ML pipeline template for building product recommendation systems. Features:

**Parameters:**
- Text embedding model selection (BAAI/BGE variants)
- Image embedding model (CLIP variants)
- LLM for review summarization (Llama 3.1, Mistral)
- S3 storage configuration
- Feast feature store toggle
- ML pipeline scheduling

**Generated Artifacts:**
- Kustomize overlays
- Model serving runtime (KServe)
- Feature store configuration
- Pipeline definitions (KFP/Argo)
- S3 credentials secrets

**Components:** Embeddings, LLM, Two-tower recommender, Feast, KServe

**Technologies:** OpenShift AI, Feast, KServe, KFP, Argo Workflows

---

### 4. Enterprise RAG Chatbot
**File:** `templates/enterprise-rag-chatbot/template.yaml`

Retrieval-Augmented Generation chatbot with vector database integration. Features:

**Parameters:**
- Vector database selection (Milvus, pgvector, Redis, Qdrant)
- LLM provider (OpenShift AI or external API)
- Embedding model configuration
- Document chunking settings
- Data source integrations (Confluence, SharePoint, Google Drive, etc.)
- Auto-sync scheduling

**Generated Artifacts:**
- Vector database deployment manifests
- Ingestion pipeline configuration
- LLM serving configuration
- Data source connectors
- Sync CronJob definitions

**Use Cases:** Internal knowledge bases, customer support, document Q&A

**Technologies:** Vector databases, Llama/Mistral, RAG pipeline

---

### 5. LLM CPU Serving
**File:** `templates/llm-cpu-serving/template.yaml`

Lightweight template for CPU-based LLM serving. Features:

**Parameters:**
- Model size selection (1B, 3B, 7B parameters)
- HuggingFace or custom model support
- Quantization options (INT4, INT8, none)
- Resource limits (CPU, memory)
- API authentication and rate limiting
- Response caching

**Generated Artifacts:**
- Deployment with resource limits
- Service and Route
- API authentication secrets
- ConfigMaps for model config

**Resource Requirements:**
- Small (1B): 2 CPU, 4GB RAM
- Medium (3B): 4 CPU, 8GB RAM
- Large (7B): 8 CPU, 16GB RAM

**Best for:** Development, testing, edge deployments, cost-sensitive workloads

---

## Key Features

### Self-Service Deployment
- Users can deploy AI applications without deep Kubernetes knowledge
- Guided forms with validation and helpful descriptions
- Sensible defaults with customization options

### GitOps Ready
- All templates generate GitOps-friendly manifests
- Optional ArgoCD Application creation
- Kustomize overlays for environment management

### Security Built-In
- Secrets management via Kubernetes Secrets
- API authentication options
- RBAC-ready namespace isolation
- Safety guardrails for LLMs (where applicable)

### Production Ready
- Resource limits and requests
- Health checks and readiness probes
- Horizontal Pod Autoscaler support
- Observability with OpenTelemetry

### Integration Friendly
- GitHub repository creation
- Backstage catalog registration
- OpenShift console links
- API documentation links

## Usage Flow

1. **Register Templates**
   - User imports `catalog-info.yaml` into Developer Hub
   - All 5 templates become available in the Create menu

2. **Select Template**
   - User browses template catalog
   - Selects appropriate AI quickstart template
   - Reads description and requirements

3. **Configure Parameters**
   - Fills out form with project details
   - Configures OpenShift cluster and namespace
   - Sets up model endpoints and credentials
   - Enables optional integrations

4. **Generate Project**
   - Template scaffolds project structure
   - Creates Kubernetes manifests
   - Optionally creates GitHub repository
   - Registers component in Backstage catalog

5. **Deploy to OpenShift**
   - User applies generated manifests
   - Or sets up GitOps with ArgoCD/Flux
   - Monitors deployment in OpenShift console
   - Accesses via generated routes

## What Makes These Templates Special

### Based on Real Red Hat AI Quickstarts
- IT Self-Service Agent: https://github.com/rh-ai-quickstart/it-self-service-agent
- LLM CPU Serving: https://github.com/rh-ai-quickstart/llm-cpu-serving
- Product Recommender: Referenced from Red Hat documentation
- Enterprise RAG: Based on common RAG patterns
- Generic: Flexible for any quickstart

### Comprehensive Parameter Coverage
- **100+ configurable parameters** across all templates
- Validation and helpful descriptions
- Conditional fields (hidden when not applicable)
- Enum selections with descriptive names

### Production-Grade Manifests
- Proper resource management
- Security best practices
- Observability hooks
- Scalability considerations

### Developer Experience
- Clear documentation
- Example values files
- Quick start guide
- Troubleshooting sections

## Technical Specifications

### Backstage Template Format
- **API Version:** `scaffolder.backstage.io/v1beta3`
- **Kind:** `Template`
- **Actions Used:**
  - `fetch:plain` - Clone GitHub repositories
  - `fetch:template` - Generate templated files
  - `publish:github` - Create GitHub repositories
  - `catalog:register` - Register Backstage components
  - `fs:rename` - File system operations

### Template Capabilities

| Capability | Generic | IT Agent | Recommender | RAG | LLM CPU |
|------------|---------|----------|-------------|-----|---------|
| GitHub Clone | ✅ | ✅ | ✅ | ✅ | ✅ |
| Kustomize | ✅ | ✅ | ✅ | ✅ | - |
| Secrets | ✅ | ✅ | ✅ | ✅ | ✅ |
| ConfigMaps | ✅ | ✅ | ✅ | ✅ | ✅ |
| ArgoCD | - | ✅ | ✅ | ✅ | - |
| Service/Route | - | ✅ | ✅ | ✅ | ✅ |
| CronJobs | - | - | ✅ | ✅ | - |
| Custom CRDs | - | ✅ | ✅ | ✅ | - |

### Prerequisites

**Required:**
- Red Hat Developer Hub (Backstage)
- OpenShift 4.17+ cluster
- GitHub account (for repo creation)

**Optional but Recommended:**
- OpenShift AI operators
- ArgoCD/OpenShift GitOps
- S3-compatible storage
- LLM API endpoints

## Example Use Cases

### Scenario 1: Development Team LLM
**Template:** LLM CPU Serving
**Time:** 5 minutes
**Use Case:** Provide developers with a lightweight LLM for code assistance

```yaml
name: dev-code-assistant
modelSize: small-1b
quantization: int8
enableAuth: true
```

### Scenario 2: Enterprise Help Desk
**Template:** IT Self-Service Agent
**Time:** 90 minutes
**Use Case:** Automate laptop refresh and IT requests

```yaml
name: helpdesk-agent
deploymentMode: production
enableSlack: true
enableServiceNow: true
```

### Scenario 3: E-Commerce Recommendations
**Template:** Product Recommender
**Time:** 30 minutes
**Use Case:** Product recommendations and review summaries

```yaml
name: shop-recommender
enableFeast: true
enablePipelines: true
llmModel: Llama 3.1 8B
```

### Scenario 4: Internal Knowledge Base
**Template:** Enterprise RAG Chatbot
**Time:** 20 minutes
**Use Case:** Answer employee questions from company docs

```yaml
name: company-kb-bot
vectorDB: milvus
dataSources: [confluence, sharepoint]
enableAutoSync: true
```

## Metrics and Validation

### Template Quality Metrics
- ✅ All templates follow Backstage best practices
- ✅ Comprehensive parameter validation
- ✅ Helpful descriptions and examples
- ✅ Proper error handling
- ✅ Security considerations
- ✅ Documentation coverage

### Testing Recommendations
1. **Dry Run:** Test template generation without deployment
2. **Dev Environment:** Deploy to dev cluster first
3. **Resource Validation:** Verify resource requests/limits
4. **Secret Management:** Test with real credentials
5. **End-to-End:** Full deployment and functionality test

## Future Enhancements

Potential additions for future versions:

1. **More Templates:**
   - Privacy-Focused AI Assistant (healthcare)
   - Computer Vision Pipeline
   - Speech-to-Text Service
   - AI Observability Summarizer

2. **Advanced Features:**
   - Multi-cluster deployment
   - Cost estimation
   - GPU scheduling
   - Model registry integration

3. **Developer Experience:**
   - Interactive CLI wizard
   - Template testing framework
   - Visual diagram generation
   - Performance benchmarking

4. **Integrations:**
   - GitLab support
   - Azure DevOps pipelines
   - Terraform modules
   - Helm chart generation

## Support and Resources

### Documentation
- **This Repository:** Complete template documentation
- **Red Hat AI Quickstarts:** https://docs.redhat.com/en/learn/ai-quickstarts
- **Developer Hub:** https://docs.redhat.com/en/documentation/red_hat_developer_hub
- **OpenShift AI:** https://docs.redhat.com/en/documentation/red_hat_openshift_ai

### Getting Help
- GitHub Issues: Report bugs or request features
- Red Hat Developer: Community forums
- Red Hat Support: Enterprise customers

### Contributing
- Fork repository
- Create feature branch
- Submit pull request
- Follow contribution guidelines

## License

Apache License 2.0

## Acknowledgments

Built on top of:
- Red Hat AI Quickstarts
- Red Hat Developer Hub (Backstage)
- OpenShift AI platform
- Kubernetes ecosystem

---

**Version:** 1.0.0
**Date:** 2026-02-04
**Status:** Production Ready
**Maintainer:** Platform Team
