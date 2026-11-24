# CloudSecOps Learning Progress

_Last consolidated: 2026-11-24 UTC._

## Learning approach
- Explain concepts and component relationships before advancing.
- Explain root cause, attack path and blast radius before remediation.
- Assess least privilege, scope, escalation, auditability and runtime enforcement.
- Use one focused hands-on exercise at a time; evaluate actual output and negative cases.
- For technical artifact reviews use: Effective Posture; High-Risk Patterns; Signal vs. Noise; Verify & Remediate.
- Track only verified outcomes; mark incomplete evidence as pending.

## Roadmap status
- **Month 1 — Reproducible Platform Foundations:** foundations covered; reproducible Git-managed platform deliverable remains in progress.
- **Month 2 — Zero-Trust Cloud-Native & Runtime Security:** in progress; Kubernetes RBAC deep dive.
- **Months 3–6:** planned.

## Established learning
- Kubernetes desired vs. actual state and controller reconciliation.
- ReplicaSets, scaling, pod deletion/replacement and scheduling constraints.
- Node labels/selectors, taints/tolerations, affinity and capacity.
- Resource requests/limits, QoS classes, OOMKill vs. eviction.
- PodDisruptionBudget intent and disruption constraints.
- RBAC Role/RoleBinding and namespace-scoped permissions.
- ServiceAccount basics and token automount behaviour.

## RBAC exercise evidence — 2026-11-23 to 2026-11-24
- Inspected ServiceAccounts `developer` and `lab-reader`; AUTOMOUNT displayed `<none>` (inherit/default, not proof of token issuance or use).
- Inspected Roles and RoleBindings in `devsecops-lab`. `developer-pod-reader` grants `get/list/watch` on Pods; `lab-reader` grants `get/list/watch` on Pods and Deployments. Each RoleBinding references its intended Role and ServiceAccount.
- Earlier authorization test matrix passed **5/5**: developer cannot read Deployments; lab-reader can read Deployments; lab-reader cannot patch Deployments; neither identity can read Secrets.
- Current context confirmed as `kubernetes-admin@kubernetes`, username `kubernetes-admin`, groups `kubeadm:cluster-admins` and `system:authenticated`; authorization output showed wildcard resource/verb permissions. Use only for administration, not as the restricted test identity.
- Namespace boundary, actual token-based authentication/use, and special-verb/escalation analysis remain pending.

## Earlier security observations requiring revalidation
- Earlier Argo CD RBAC output contained broad wildcard permissions and a high-privilege application-controller binding. Reinspect current objects before drawing conclusions or changing them.
- Reconcile identity, kubeconfig context, namespace and command scope when authorization outputs differ.

## Evaluation record
- **Criterion:** Interpret Role rules, RoleBinding subjects/roleRefs, and effective authorization.
- **Result:** Role/RoleBinding inspection completed; prior 5/5 authorization checks passed.
- **Takeaway:** Role rules define resource/verb permissions; RoleBinding attaches them to a subject in a namespace. A privileged admin context must not be confused with the restricted ServiceAccount.
- **Next checkpoint:** ClusterRole vs. ClusterRoleBinding, then `bind`, `escalate`, and `impersonate` safeguards.

## Evidence discipline
Record date, identity/context, namespace, command purpose, sanitized result and pass/fail. Never record bearer tokens, full kubeconfig, private keys, passwords or live Secret data.
