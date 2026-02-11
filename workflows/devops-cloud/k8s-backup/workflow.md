# k8s-backup

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/rohitg00/k8s-backup/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/rohitg00/k8s-backup/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Kubernetes backup and restore with Velero. Use when creating backups, restoring applications, managing disaster recovery, or migrating workloads between clusters.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Kubernetes backup and restore with Velero. Use when creating backups, restoring applications, managing disaster recovery, or migrating workloads between clusters.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run k8s-backup`)
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
You are executing the k8s-backup workflow. Use the following context:

Description: Kubernetes backup and restore with Velero. Use when creating backups, restoring applications, managing disaster recovery, or migrating workloads between clusters.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: k8s-backup
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Kubernetes Backup with Velero

Manage backups and restores using kubectl-mcp-server's Velero tools.

## Check Velero Installation

```python
# Detect Velero
velero_detect_tool()

# List backup locations
velero_backup_locations_list_tool()
```

## Create Backups

```python
# Backup entire namespace
velero_backup_create_tool(
    name="my-backup",
    namespaces=["default", "app-namespace"]
)

# Backup with label selector
velero_backup_create_tool(
    name="app-backup",
    namespaces=["default"],
    label_selector="app=my-app"
)

# Backup excluding resources
velero_backup_create_tool(
    name="config-backup",
    namespaces=["default"],
    exclude_resources=["pods", "replicasets"]
)

# Backup with TTL
velero_backup_create_tool(
    name="daily-backup",
    namespaces=["production"],
    ttl="720h"  # 30 days
)
```

## List and Describe Backups

```python
# List all backups
velero_backups_list_tool()

# Get backup details
velero_backup_get_tool(name="my-backup")

# Check backup status
# - New: Backup request created
# - InProgress: Backup running
# - Completed: Backup successful
# - Failed: Backup failed
# - PartiallyFailed: Some items failed
```

## Restore from Backup

```python
# Full restore
velero_restore_create_tool(
    name="my-restore",
    backup_name="my-backup"
)

# Restore to different namespace
velero_restore_create_tool(
    name="my-restore",
    backup_name="my-backup",
    namespace_mappings={"old-ns": "new-ns"}
)

# Restore specific resources
velero_restore_create_tool(
    name="config-restore",
    backup_name="my-backup",
    include_resources=["configmaps", "secrets"]
)

# Restore excluding resources
velero_restore_create_tool(
    name="partial-restore",
    backup_name="my-backup",
    exclude_resources=["persistentvolumeclaims"]
)
```

## List and Monitor Restores

```python
# List restores
velero_restores_list_tool()

# Get restore details
velero_restore_get_tool(name="my-restore")
```

## Scheduled Backups

```python
# List schedules
velero_schedules_list_tool()

# Get schedule details
velero_schedule_get_tool(name="daily-backup")

# Create schedule (via kubectl)
kubectl_apply(manifest="""
apiVersion: velero.io/v1
kind: Schedule
metadata:
  name: daily-backup
  namespace: velero
spec:
  schedule: "0 2 * * *"  # 2 AM daily
  template:
    includedNamespaces:
    - production
    ttl: 720h
""")
```

## Disaster Recovery Workflow

### Create DR Backup
```python
1. velero_backup_create_tool(
       name="dr-backup-$(date)",
       namespaces=["production"]
   )
2. velero_backup_get_tool(name="dr-backup-...")  # Wait for completion
```

### Restore to New Cluster
```python
1. velero_detect_tool()  # Verify Velero installed
2. velero_backups_list_tool()  # Find backup
3. velero_restore_create_tool(
       name="dr-restore",
       backup_name="dr-backup-..."
   )
4. velero_restore_get_tool(name="dr-restore")  # Monitor
```

## Related Skills

- [k8s-multicluster](../k8s-multicluster/SKILL.md) - Multi-cluster operations
- [k8s-incident](../k8s-incident/SKILL.md) - Incident response

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
