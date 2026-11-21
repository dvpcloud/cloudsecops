# Learning Roadmap

## Phase 0 — Workstation and access

- [ ] Establish host-to-`k8smaster` network connectivity.
- [ ] Confirm TCP access to Kubernetes API port 6443.
- [ ] Install/check kubectl and Git on the host.
- [ ] Transfer a bootstrap kubeconfig securely; protect it and keep it out of Git.
- [ ] Verify `kubectl get nodes` from the host.
- [ ] Create a least-privilege DevSecOps identity and RBAC (do not use cluster-admin for routine work).
- [ ] Record sanitized verification results.

## Phase 1 — Kubernetes foundations

- [ ] Namespaces, Pods, Deployments, ReplicaSets
- [ ] Services, DNS, ingress/gateway concepts
- [ ] ConfigMaps and Secrets (safe handling)
- [ ] Probes, resource requests/limits, scheduling
- [ ] Troubleshooting and cleanup

## Phase 2 — Kubernetes security

- [ ] RBAC and service accounts
- [ ] Pod Security Standards
- [ ] NetworkPolicy with Calico
- [ ] Admission controls / policy as code (Kyverno or equivalent)
- [ ] Image provenance, scanning, and runtime controls
- [ ] Audit logging and security posture review

## Phase 3 — DevSecOps delivery

- [ ] Git-based workflow and pull requests
- [ ] Argo CD / GitOps
- [ ] CI pipeline with linting and tests
- [ ] Container image build and vulnerability scanning
- [ ] Secret management integration
- [ ] Supply-chain security and SBOM

## Phase 4 — Infrastructure automation

- [ ] Terraform fundamentals and safe state management
- [ ] Ansible for host configuration
- [ ] Reusable scripts with validation and error handling
- [ ] Idempotent environment setup and teardown

## Phase 5 — Cloud SecOps

- [ ] Threat modeling and attack surface
- [ ] Detection engineering and alert triage
- [ ] Falco or equivalent runtime detection
- [ ] Incident response exercises
- [ ] Evidence collection and reporting

## Definition of done for each exercise

1. Prerequisites are documented.
2. Files are committed in the appropriate directory.
3. Commands and expected results are recorded.
4. Security considerations and cleanup are included.
5. Validation has been run or explicitly marked pending.
