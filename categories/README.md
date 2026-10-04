# Custom RHACS Policy Categories

## Parasol Secured Build Gate

This category is created automatically by the RHACS setup job
(`cluster/rhacs/rhacs-central/templates/job-policy-category.yaml`)
during cluster provisioning.

RHACS does not support creating categories via Kubernetes CRDs.
The category is created via the Central API:

```
POST /v1/policycategories
{"name": "Parasol Secured Build Gate"}
```

The category must exist before SecurityPolicy CRs that reference it
can be applied.
