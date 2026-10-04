# ACS Policies as Code

SecurityPolicy custom resources for Red Hat Advanced Cluster Security (RHACS).
These policies are deployed to the cluster via ArgoCD and applied as Kubernetes
resources using the `config.stackrox.io/v1alpha1` SecurityPolicy CRD.

## Structure

```
acs-policies/
├── policies/         # SecurityPolicy CRs (applied via oc apply / ArgoCD)
│   ├── curl-in-image.yaml
│   ├── fixable-severity-at-least-important.yaml
│   └── ...
├── categories/       # Custom category documentation
│   └── README.md
└── README.md
```

## Category: Parasol Secured Build Gate

All policies in this repo are assigned to the custom category
`Parasol Secured Build Gate`. This category must exist in RHACS Central
before the policies can be applied — it is created automatically by the
RHACS setup job in the gitops repo.

The secured pipeline uses `roxctl image check --categories="Parasol Secured Build Gate"`
to evaluate only these policies, keeping them separate from the default
RHACS policy set.

## Adding a New Policy

1. Export the policy from RHACS as JSON (or write from scratch)
2. Create a SecurityPolicy CR YAML in `policies/`
3. Set `spec.categories` to `["Parasol Secured Build Gate"]`
4. Set `spec.lifecycleStages` to `["BUILD"]`
5. Set `spec.enforcementActions` to `["FAIL_BUILD_ENFORCEMENT"]`
6. Push to `module2` branch
