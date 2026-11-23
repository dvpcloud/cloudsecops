# CloudSecOps Learning Progress

_Last consolidated: 2026-11-23 UTC._

## Learning approach
- Explain concepts and component relationships before advancing.
- Explain root cause, attack path and blast radius before remediation.
- Assess least privilege, scope, escalation, auditability and runtime enforcement.
- Use one focused hands-on exercise at a time; evaluate actual output and negative cases.
- For technical artifact reviews use: Effective Posture; High-Risk Patterns; Signal vs. Noise; Verify & Remediate.
- Track only verified outcomes; mark incomplete evidence as pending.

## Roadmap status
- **Month 1 — Reproducible Platform Foundations:** foundations covered; reproducible Git-managed platform deliverable remains in progress.
- **Month 2 — Zero-Trust Cloud-Native & Runtime Security:** in progress; current focus Kubernetes RBAC.
- **Months 3–6:** planned.

## Established learning
- Kubernetes desired vs. actual state and controller reconciliation.
- ReplicaSets, scaling, pod deletion/replacement and scheduling constraints.
- Node labels/selectors, taints/tolerations, affinity and capacity.
- Resource requests/limits, QoS classes, OOMKill vs. eviction.
- PodDisruptionBudget intent and disruption constraints.
- RBAC Role/RoleBinding and namespace-scoped permissions.
- ServiceAccount basics and token automount behaviour.

## RBAC exercise evidence — 2026-11-23
- Reviewed RoleBinding `developer-pod-reader-binding` in `devsecops-lab`.
- Effective Role rules shown in the exercise: `get`, `list`, `watch` on `pods` and `deployments.apps`. This is read-only access to those resource types within the Role's namespace.
- Inspected ServiceAccounts `developer` and `lab-reader`; displayed AUTOMOUNT as `<none>` (inherit/default, not proof of token issuance or token use).
- User reported no Pods were running under those ServiceAccounts at the time.
- User correctly identified that the Role permits reading/listing/watching Pods and Deployments, not arbitrary resources or write actions.
- Verification of effective access as each ServiceAccount, namespace boundaries, token projection and escalation protections remains pending.

## Earlier security observations requiring revalidation
- Earlier output identified the current caller as `kubernetes-admin` and showed broad cluster-admin-like authorization checks. Do not assume the same identity/context is active now.
- Earlier Argo CD RBAC output contained broad wildcard permissions and a high-privilege application-controller binding. Reinspect current objects before drawing conclusions or changing them.
- A prior SelfSubjectRules output appeared narrower than separate authorization checks. Reconcile identity, kubeconfig context, namespace and command scope before relying on either result.

## Evaluation record
- **Criterion:** Interpret Role rules and the bound resource scope.
- **Result:** Correctly identified read-only verbs on Pods and Deployments.
- **Takeaway:** Role rules constrain both resource types and verbs; the RoleBinding determines which subject receives them and in which namespace.
- **Next validation:** Test allowed and denied actions using the intended restricted identity, then verify cross-namespace denial.

## Evidence discipline
Record date, identity/context, namespace, command purpose, sanitized result and pass/fail. Never record bearer tokens, full kubeconfig, private keys, passwords or live Secret data.
