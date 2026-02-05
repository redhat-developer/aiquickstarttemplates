# Quick Start Guide

Get started with Red Hat AI Quickstart templates in 5 minutes!

## Prerequisites

- Red Hat Developer Hub installed
- OpenShift cluster access
- `oc` CLI tool installed

## Step 1: Register Templates (1 minute)

### Method 1: UI Registration

1. Open Developer Hub
2. Navigate to **Create** → **Register Existing Component**
3. Enter your repository URL:
   ```
   https://github.com/YOUR-ORG/aiquickstart/blob/main/catalog-info.yaml
   ```
4. Click **Import**

### Method 2: CLI Registration

```bash
# Clone the repository
git clone https://github.com/YOUR-ORG/aiquickstart.git
cd aiquickstart

# Register with Developer Hub
curl -X POST http://your-developer-hub/api/catalog/locations \
  -H "Content-Type: application/json" \
  -d '{"type": "url", "target": "https://github.com/YOUR-ORG/aiquickstart/blob/main/catalog-info.yaml"}'
```

## Step 2: Create Your First AI Quickstart (3 minutes)

Let's deploy the **LLM CPU Serving** quickstart - the simplest to get started:

1. Go to **Create** in Developer Hub
2. Search for "LLM CPU Serving"
3. Fill in the form:

   **Project Information:**
   - Name: `my-first-llm`
   - Owner: Select your team/user
   - Description: `Testing LLM CPU serving`

   **Deployment Configuration:**
   - OpenShift Cluster: `https://api.your-cluster.com:6443`
   - Namespace: `llm-demo`

   **Model Configuration:**
   - Model Size: `Small (1B)` (lightest option)
   - Model Source: `HuggingFace Hub`
   - HuggingFace Model: `TinyLlama/TinyLlama-1.1B-Chat-v1.0` (default)
   - Quantization: `INT8`

   **Leave other settings as defaults**

4. Click **Review and Create**

## Step 3: Deploy to OpenShift (1 minute)

The template created a GitHub repository with all the manifests. Now deploy it:

```bash
# Clone the generated repository
git clone <your-generated-repo-url>
cd my-first-llm

# Login to OpenShift
oc login --token=<your-token> --server=https://api.your-cluster.com:6443

# Create namespace
oc new-project llm-demo

# Deploy
oc apply -k manifests/

# Watch the deployment
oc get pods -n llm-demo -w
```

## Step 4: Test Your LLM (30 seconds)

```bash
# Get the route URL
export LLM_URL=$(oc get route my-first-llm -n llm-demo -o jsonpath='{.spec.host}')

# Test the endpoint
curl https://$LLM_URL/v1/completions \
  -H "Content-Type: application/json" \
  -d '{
    "prompt": "What is OpenShift?",
    "max_tokens": 100
  }'
```

Expected response:
```json
{
  "id": "cmpl-xxx",
  "object": "text_completion",
  "created": 1234567890,
  "model": "TinyLlama/TinyLlama-1.1B-Chat-v1.0",
  "choices": [{
    "text": "OpenShift is a Kubernetes-based container platform...",
    "index": 0,
    "finish_reason": "stop"
  }]
}
```

## Next Steps

### Try More Complex Templates

Now that you've deployed your first quickstart, try these:

#### 1. Enterprise RAG Chatbot
Deploy a chatbot with company knowledge:
```bash
# Uses vector database + LLM
# Good for: Internal Q&A, documentation search
# Time: ~15 minutes
```

#### 2. IT Self-Service Agent
Deploy an agentic AI system:
```bash
# Requires: Llama 3 70B endpoint
# Good for: IT automation, helpdesk
# Time: ~60-90 minutes
```

#### 3. Product Recommender
Build a recommendation system:
```bash
# Requires: S3 storage, multiple models
# Good for: E-commerce, content platforms
# Time: ~30 minutes
```

### Customize Your Deployment

Edit the generated manifests:
```bash
cd my-first-llm

# Increase resources
vi manifests/deployment.yaml
# Update CPU/memory limits

# Enable authentication
vi manifests/secret.yaml
# Add API keys

# Redeploy
oc apply -k manifests/
```

### Monitor Performance

```bash
# Check pod status
oc get pods -n llm-demo

# View logs
oc logs -f deployment/my-first-llm -n llm-demo

# Check resource usage
oc adm top pods -n llm-demo

# Access metrics
oc get --raw /apis/metrics.k8s.io/v1beta1/namespaces/llm-demo/pods
```

### Scale Your Service

```bash
# Manual scaling
oc scale deployment/my-first-llm --replicas=3 -n llm-demo

# Auto-scaling (HPA)
oc autoscale deployment/my-first-llm \
  --min=1 --max=5 \
  --cpu-percent=70 \
  -n llm-demo
```

## Troubleshooting

### Pod Not Starting

```bash
# Check pod status
oc describe pod -l app=my-first-llm -n llm-demo

# Common issues:
# - Image pull errors: Check network/registry access
# - Resource limits: Increase CPU/memory
# - Model download timeout: Wait longer or use smaller model
```

### API Endpoint Not Responding

```bash
# Check route
oc get route my-first-llm -n llm-demo

# Test service directly
oc port-forward svc/my-first-llm 8080:8080 -n llm-demo
curl http://localhost:8080/health

# Check logs
oc logs -f deployment/my-first-llm -n llm-demo
```

### Out of Memory

```bash
# Increase memory limits
oc set resources deployment/my-first-llm \
  --limits=memory=16Gi \
  --requests=memory=8Gi \
  -n llm-demo

# Or use smaller model/quantization
# Edit template and recreate
```

## Clean Up

When done testing:

```bash
# Delete the deployment
oc delete project llm-demo

# Optionally delete the GitHub repository
# (Use GitHub UI or gh CLI)
```

## Additional Resources

- **Full Documentation:** See [README.md](README.md)
- **Template Reference:** Check individual template files in `templates/`
- **Red Hat AI Docs:** https://docs.redhat.com/en/learn/ai-quickstarts
- **Developer Hub Docs:** https://docs.redhat.com/en/documentation/red_hat_developer_hub

## Get Help

- File issues in this repository
- Check Red Hat Developer forums
- Contact Red Hat support (enterprise customers)

---

**Congratulations!** You've deployed your first AI quickstart. Explore the other templates to build more complex AI applications.
