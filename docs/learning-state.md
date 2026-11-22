# CloudSecOps Learning State

_Last consolidated: 2026-11-22 (UTC)_

This file is the durable continuity record for the CloudSecOps learning project. Update it after meaningful lessons, lab changes, verified exercises, or milestone completion. Do not store credentials, kubeconfig contents, tokens, private keys, or live Secret values here.

## Operating approach

- Mentor stance: CloudSecOps mentor / principal security engineer.
- Pace: intensive; teaching style: balanced conceptual explanation and hands-on work.
- Explain unfamiliar mechanics before commands; explain threat path, blast radius, and rationale before remediation.
- Work incrementally: one focused exercise at a time, inspect actual output before progressing.
- Assess identity, permissions, scope, escalation paths, blast radius, auditability, runtime enforcement, and verification.
- For CLI/manifests/logs, structure assessments as: Effective Posture; High-Risk Patterns; Signal vs. Noise; Verify & Remediate.
- Use host Ubuntu workstation for Git, kubectl, Helm, Terraform and security tooling; do not use the control-plane VM as the primary workstation.
- Preserve the existing cluster. Avoid destructive resets or unnecessary changes.
- Track tested artifacts in GitHub. Review diffs and exclude secrets and sensitive state; maintain appropriate .gitignore rules.
- Prefer practical, reproducible exercises with prerequisites, expected output, validation, cleanup/rollback, and troubleshooting.
- Keep explanations concise, avoid repeating completed material, and mark assumptions or unverified facts.

## Six-month target roadmap

1. **Month 1 — Reproducible platform foundations:** Kubernetes administration, Helm, CNI, Terraform, Argo CD/GitOps, GitHub Actions, Python automation, drift remediation, multi-environment overlays, OIDC federation. Deliverable: reproducible Git-managed platform.
2. **Month 2 — Zero-trust cloud-native and runtime security:** RBAC, Gateway API, NetworkPolicy, external secrets, observability, Kyverno/OPA, image signing, SPIFFE/SPIRE, Cilium/Tetragon, SLSA/SBOM/Cosign. Deliverable: zero-trust Kubernetes platform with runtime telemetry and supply-chain gates.
3. **Month 3 — AI and inference platform engineering:** LLM APIs, FastAPI, RAG, vector databases, model serving, evaluation, observability, GPU/FinOps controls, tenant isolation. Deliverable: instrumented, cost-controlled RAG application on Kubernetes.
4. **Month 4 — Adversarial AI security and governance:** prompt injection, data leakage, excessive permissions, model/data supply chain, API security, RAG ACLs, red teaming, model integrity, AI gateway controls. Deliverable: threat-modeled AI application with adversarial tests.
5. **Month 5 — Agentic SecOps and sandboxed autonomy:** agent/tool calling, MCP, identity and per-tool authorization, human approval, sandboxing, incident investigation, detection engineering, signed approvals. Deliverable: sandboxed SecOps assistant without unrestricted production mutation.
6. **Month 6 — Cloud production, resilience and career positioning:** AWS/GCP deployment, CI/CD gates, cost, reliability, DR, monitoring, IR, architecture records, chaos/game days, runtime-to-CI feedback. Deliverable: portfolio-grade AI-resilient CloudSecOps platform.

## Lab baseline

_Last observed in project conversation; re-verify before relying on it._

- Existing 3-node Kubernetes cluster, preserved during the project reset.
- Kubernetes version reported as v1.36.6 on all nodes.
- Control plane: `k8smaster`, internal IP `192.168.122.105`, API endpoint `https://192.168.122.105:6443`.
- Workers: `k8sworker1` (`192.168.122.87`) and `k8sworker2` (`192.168.122.232`).
- OS reported: Ubuntu 26.04.1 LTS; containerd 2.2.2.
- Components previously observed: Calico, MetalLB, Envoy Gateway, Argo CD.
- Project namespace: `devsecops-lab`, labels include `environment=lab`, `owner=devsecops`, `purpose=cloud-secops-learning`.
- Argo CD controllers/components were present and Ready in the latest recorded inspection; no Argo CD Applications or ApplicationSets were present after the project reset.
- Host-to-API network reachability and TCP/6443 connectivity were tested successfully. A Kubernetes identity was subsequently observed from the host; current kubeconfig/authentication state should be rechecked when needed.
- Never assume this snapshot is current; inspect before changing cluster resources.

## Learning progress and evidence

### Completed / established

- Preserved the existing cluster while resetting/reorganizing the learning project.
- Established host-based Kubernetes administration as the intended workflow; tested network reachability to the API endpoint.
- Reviewed Kubernetes foundations including desired vs. actual state, controllers, scheduling, node affinity/tolerations, resources, QoS, and PodDisruptionBudgets in earlier learning.
- Began the current structured CloudSecOps roadmap and RBAC deep dive.
- Identified current Kubernetes caller in prior output:
  - Username: `kubernetes-admin`
  - Groups: `kubeadm:cluster-admins`, `system:authenticated`
- Prior authorization checks returned **yes** for:
  - `kubectl auth can-i '*' '*' --all-namespaces`
  - `kubectl auth can-i get secrets --all-namespaces`
  - `kubectl auth can-i create clusterrolebindings`
- Reviewed Argo CD ClusterRoles. The `argocd-application-controller` role showed broad wildcard permissions in the captured output; an Argo CD application-controller cluster-admin-level ClusterRoleBinding was also observed. Treat as high-risk/broad privilege requiring contextual review, not as automatically exploitable.
- A targeted SelfSubjectRules review previously showed Pod read verbs (`get/list/watch`) and limited API discovery/health GET access for the inspected identity/context. This does not supersede the broad `kubernetes-admin` authorization checks; the outputs may have been collected under different identities or scopes and must be reconciled.

### Current position

**Kubernetes RBAC Deep Dive — Part 2: privilege-escalation safeguards.**

The next learning objective is to understand how Kubernetes prevents privilege escalation when identities create or modify Roles, ClusterRoles, RoleBindings, and ClusterRoleBindings. No RBAC mutations have been authorized as part of this exercise.

### Outstanding work

1. Inspect and explain Kubernetes authorization checks and RBAC escalation safeguards: `bind`, `escalate`, and `impersonate`.
2. Reconcile current identity, groups, kubeconfig context, and effective permissions.
3. Inspect the specific binding chain that grants `kubernetes-admin` its privileges; identify subjects, roleRef, and scope.
4. Create a dedicated restricted test identity (not cluster-admin) and validate both allowed and denied operations.
5. Test namespace boundaries and privilege-escalation protections without granting unnecessary cluster-wide permissions.
6. Continue into ServiceAccount security, least-privilege design, RBAC auditing, and drift detection.
7. Update this file and relevant exercise documentation with sanitized evidence as work is completed.

## Evidence and update rules

- Separate **observed**, **inferred**, and **not yet verified** facts.
- Record date, context/identity, namespace/scope, command purpose, sanitized result, and validation status.
- Never paste secrets, full kubeconfig data, bearer tokens, private keys, or sensitive Secret values.
- Do not mark an exercise complete until its expected behavior and negative cases have been tested.
- Keep this state file concise; put detailed procedures and manifests in their relevant exercise directories.
