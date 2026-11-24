# CloudSecOps Next Steps

_Last updated: 2026-11-24 UTC._

## Current checkpoint — Kubernetes RBAC Deep Dive Part 2
Previously completed; do not repeat unless evidence changes:
- Identity/context inspection.
- Role and RoleBinding inspection for `developer-pod-reader` / `developer` and `lab-reader` / `lab-reader`.
- Authorization matrix: 5/5 passed (developer Deployments read denied; lab-reader Deployments read allowed; lab-reader Deployment patch denied; Secrets read denied for both).

Current admin context is `kubernetes-admin@kubernetes` with wildcard permissions. Preserve it for administration only; do not use it as the restricted test identity.

## Next learning sequence
1. **ClusterRole vs. ClusterRoleBinding**
   - ClusterRole can define cluster-wide permissions or reusable resource rules.
   - RoleBinding can bind a Role or ClusterRole within one namespace; ClusterRoleBinding grants the referenced ClusterRole cluster-wide.
   - Review scope and blast radius with examples before making changes.

2. **RBAC privilege-escalation safeguards**
   - Learn and inspect special verbs: `bind`, `escalate`, and `impersonate`.
   - Explain how Kubernetes prevents users from granting permissions they do not already possess, except where relevant special authority exists.
   - Inspect who can create/update Roles, ClusterRoles, RoleBindings and ClusterRoleBindings. No broad grants or mutations for the exercise.

3. **Namespace boundary and token security**
   - Namespace-boundary authorization test remains pending.
   - Distinguish ServiceAccount API permissions from token mounting/authentication.
   - Inspect ServiceAccount and Pod automount settings and projected token metadata without printing token contents.

4. **Record verified results**
   - Update progress only after new tests pass.
   - Add a focused exercise under `security/rbac/` when stable.

## After RBAC
- Pod Security Standards and admission policy (Kyverno/OPA).
- Calico NetworkPolicy and default-deny design.
- Audit logging and runtime detection.
- Image provenance, SBOM and Cosign.
- Later roadmap stages: SPIFFE/SPIRE, Cilium/eBPF/Tetragon, SLSA, AI platform and agent/MCP security.

## Safety constraints
- Preserve the existing cluster; no destructive resets or broad privilege grants.
- Never expose credentials, kubeconfig, tokens or live Secret values.
- Inspect live state before applying manifests.
- Include expected allowed and denied cases in each new permission test.
