# CloudSecOps Next Steps

_Last updated: 2026-11-23 UTC._

## Active exercise — Kubernetes RBAC Deep Dive Part 2
Work in the existing lab and preserve cluster state. Do not use cluster-admin as the test identity.

1. **Reconcile identity and context**
   - Inspect `kubectl config current-context` and `kubectl auth whoami` (where supported).
   - Record the active user and groups without exposing kubeconfig contents.
   - Confirm the target namespace is `devsecops-lab`.

2. **Verify the intended ServiceAccount permissions**
   - Use `kubectl auth can-i` with `--as=system:serviceaccount:devsecops-lab:developer` and the relevant namespace.
   - Confirm allowed reads of Pods and Deployments.
   - Confirm denied writes (for example create/delete Pods) and access to unrelated resources (for example Secrets).
   - If impersonation is denied, do not grant it just to complete the test; use an authorized test identity or ask for the exact sanitized error.

3. **Understand escalation controls**
   - Study Kubernetes RBAC special verbs: `bind`, `escalate`, and `impersonate`.
   - Inspect who can create/update Roles, ClusterRoles, RoleBindings and ClusterRoleBindings.
   - Explain how Kubernetes prevents a principal from granting permissions it does not already hold, unless it has the relevant escalation/bind authority.

4. **Check scope and bindings**
   - Inspect the Role, RoleBinding, subjects and `roleRef`.
   - Compare RoleBinding with ClusterRoleBinding.
   - Test namespace isolation using a second namespace only if a safe test namespace is available.

5. **ServiceAccount token security**
   - Distinguish the ServiceAccount's API permissions from whether a Pod receives a token.
   - Inspect `automountServiceAccountToken` at ServiceAccount and Pod level, projected token behaviour and token audience/expiry.
   - Do not print or share token contents.

6. **Record results**
   - Capture sanitized allowed/denied checks.
   - Update [LEARNING_PROGRESS.md](LEARNING_PROGRESS.md) only after tests pass.
   - Add a focused exercise document under `security/rbac/` when the procedure is stable.

## After RBAC
- Pod Security Standards and admission policy (Kyverno/OPA).
- Calico NetworkPolicy and default-deny design.
- Audit logging and runtime detection.
- Image provenance, SBOM and Cosign.
- Later roadmap stages: SPIFFE/SPIRE, Cilium/eBPF/Tetragon, SLSA, AI platform and agent/MCP security.

## Safety constraints
- No destructive cluster resets or broad privilege grants.
- Never expose credentials, kubeconfig, tokens or live Secret values.
- Inspect live state before applying manifests.
- Every permission test must include expected allowed and denied cases.
