# k8-multicluster

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/rohitg00/k8-multicluster/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/rohitg00/k8-multicluster/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Manage multiple Kubernetes clusters, switch contexts, and perform cross-cluster operations. Use when working with multiple clusters, comparing environments, or managing cluster lifecycle.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Manage multiple Kubernetes clusters, switch contexts, and perform cross-cluster operations. Use when working with multiple clusters, comparing environments, or managing cluster lifecycle.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run k8-multicluster`)
**Workflow:** Execute skill logic with context from AiDarr's ATLAS memory

### T - Tools
Required tools (add as needed):
- HTTP requests (for API calls)
- Memory system (ATLAS for persistence)
- Context retrieval (from GOTCHA workspace)

### C - Context
Required context sources:
- User preferences from ATLAS memory
- Relevant documents from workspace
- Historical execution data

### H - Hard Prompts

```prompt
You are executing the k8-multicluster workflow. Use the following context:

Description: Manage multiple Kubernetes clusters, switch contexts, and perform cross-cluster operations. Use when working with multiple clusters, comparing environments, or managing cluster lifecycle.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: k8-multicluster
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Multi-Cluster Kubernetes Management

Cross-cluster operations and context management using kubectl-mcp-server's multi-cluster support.

## Context Management

### List Available Contexts
```
list_contexts_tool()
```

### View Current Context
```
kubeconfig_view()  # Shows sanitized kubeconfig
```

### Switch Context
CLI: `kubectl-mcp-server context <context-name>`

## Cross-Cluster Operations

All kubectl-mcp-server tools support the `context` parameter:

```python
# Get pods from production cluster
get_pods(namespace="default", context="production-cluster")

# Get pods from staging cluster
get_pods(namespace="default", context="staging-cluster")
```

## Common Multi-Cluster Patterns

### Compare Environments

```
# Compare deployment across clusters
compare_namespaces(
    namespace1="production",
    namespace2="staging",
    resource_type="deployment",
    context="production-cluster"
)
```

### Parallel Queries
Query multiple clusters simultaneously:

```
# Production cluster
get_pods(namespace="app", context="prod-us-east")
get_pods(namespace="app", context="prod-eu-west")

# Development cluster
get_pods(namespace="app", context="development")
```

### Cross-Cluster Health Check
```
# Check all clusters
for context in ["prod-1", "prod-2", "staging"]:
    get_nodes(context=context)
    get_pods(namespace="kube-system", context=context)
```

## Cluster API (CAPI) Management

For managing cluster lifecycle:

### List Managed Clusters
```
capi_clusters_list_tool(namespace="capi-system")
```

### Get Cluster Details
```
capi_cluster_get_tool(name="prod-cluster", namespace="capi-system")
```

### Get Workload Cluster Kubeconfig
```
capi_cluster_kubeconfig_tool(name="prod-cluster", namespace="capi-system")
```

### Machine Management
```
capi_machines_list_tool(namespace="capi-system")
capi_machinedeployments_list_tool(namespace="capi-system")
```

### Scale Cluster
```
capi_machinedeployment_scale_tool(
    name="prod-cluster-md-0",
    namespace="capi-system",
    replicas=5
)
```

See [CONTEXT-SWITCHING.md](CONTEXT-SWITCHING.md) for detailed patterns.

## Multi-Cluster Helm

Deploy charts to specific clusters:
```
install_helm_chart(
    name="nginx",
    chart="bitnami/nginx",
    namespace="web",
    context="production-cluster"
)

list_helm_releases(
    namespace="web",
    context="staging-cluster"
)
```

## Multi-Cluster GitOps

### Flux Across Clusters
```
flux_kustomizations_list_tool(
    namespace="flux-system",
    context="cluster-1"
)

flux_reconcile_tool(
    kind="kustomization",
    name="apps",
    namespace="flux-system",
    context="cluster-2"
)
```

### ArgoCD Across Clusters
```
argocd_apps_list_tool(namespace="argocd", context="management-cluster")
```

## Federation Patterns

### Secret Synchronization
```
# Read from source cluster
get_secrets(namespace="app", context="source-cluster")

# Apply to target cluster (via manifest)
apply_manifest(secret_manifest, namespace="app", context="target-cluster")
```

### Cross-Cluster Service Discovery
With Cilium ClusterMesh or Istio multi-cluster:
```
cilium_nodes_list_tool(context="cluster-1")
istio_proxy_status_tool(context="cluster-2")
```

## Best Practices

1. **Naming Convention**: Use descriptive context names
   - `prod-us-east-1`, `staging-eu-west-1`

2. **Access Control**: Different kubeconfigs per environment
   - Prod: Read-only for most users
   - Dev: Full access for developers

3. **Always Specify Context**: Avoid accidental cross-cluster operations
   ```
   # Explicit is better
   get_pods(namespace="app", context="production")
   ```

4. **Cluster Groups**: Organize by purpose
   - Production: `prod-*`
   - Staging: `staging-*`
   - Development: `dev-*`

## Related Skills
- [k8s-troubleshoot](../k8s-troubleshoot/SKILL.md) - Debug across clusters
- [k8s-gitops](../k8s-gitops/SKILL.md) - GitOps multi-cluster

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
