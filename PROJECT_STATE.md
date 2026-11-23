# CloudSecOps Project State

_Last verified from project records and user-provided lab output: 2026-11-23 UTC._

## Purpose
Build practical, job-ready CloudSecOps capability across cloud infrastructure, Kubernetes, CI/CD, IAM/RBAC, threat detection, AI security and remediation. Follow the six-month roadmap in [ROADMAP.md](ROADMAP.md).

## Lab environment
**Observed in the latest supplied cluster inventory (2026-11-14; re-verify before operational changes):**
- Three Ubuntu VMs: `k8smaster` control plane, `k8sworker1`, `k8sworker2`.
- Kubernetes v1.36.6; containerd 2.2.2; Ubuntu 26.04.1 LTS.
- Node addresses: control plane `192.168.122.105`, worker1 `192.168.122.87`, worker2 `192.168.122.232`.
- API endpoint: `https://192.168.122.105:6443`.
- Components previously observed: Calico/Tigera Operator, MetalLB, Argo CD, Envoy Gateway.
- Project namespace: `devsecops-lab` (created after preserving the existing cluster and resetting project resources).
- Argo CD Applications and ApplicationSets were empty in the last recorded check.
- No StorageClasses or PVCs were present in the last recorded check.

**Operational assumptions and safeguards**
- Preserve the existing cluster; no clean-slate rebuild.
- Use the Ubuntu host as the primary workstation; do not use the control-plane VM as the project workstation.
- Inspect live state before every change. The above inventory is a snapshot, not a claim about current state.
- Use a restricted identity for routine work; do not normalize cluster-admin access.
- No credentials, kubeconfig content, tokens, private keys, live Secret values or sensitive Terraform state belong in this repository.

## Current technical focus
Kubernetes RBAC Deep Dive, continuing from Part 2. Current namespace used in exercises: `devsecops-lab`.

## Repository conventions
- This file records environment and architecture state.
- [LEARNING_PROGRESS.md](LEARNING_PROGRESS.md) records completed work and evaluation evidence.
- [NEXT_STEPS.md](NEXT_STEPS.md) records the active queue.
- [ROADMAP.md](ROADMAP.md) remains the six-month curriculum.
- Inspect existing files, make small reviewable changes, run validation, and obtain authorization before pushing.
- Keep observed facts distinct from assumptions and pending verification.
