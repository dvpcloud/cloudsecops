# Cloud SecOps Learning Path

A practical, version-controlled learning environment for Kubernetes, cloud security, DevSecOps automation, and security operations.

## Lab approach

- **Host workstation:** source code, Git, kubectl, Helm, Terraform, Ansible, security tools, and exercises.
- **Kubernetes control plane:** the existing `k8smaster` VM runs the cluster control plane; avoid using it as the primary project workstation.
- **Remote administration:** kubectl on the host communicates with the Kubernetes API over HTTPS using kubeconfig.
- **GitHub:** canonical reference for tested manifests, scripts, notes, architecture, and repeatable exercises.

## Current lab context

This repository documents the lab as observed in the project conversation (November 2026). Verify before relying on it because cluster state may change.

- Kubernetes control-plane node: `k8smaster`
- API endpoint intended for host access: `192.168.122.105:6443`
- Existing cluster components mentioned: Argo CD, Calico, Envoy Gateway
- Project namespace: `devsecops-lab`
- Decision: preserve the existing cluster while resetting/reorganizing the learning project.

## Start here

1. Read [the roadmap](ROADMAP.md).
2. Review [lab architecture](docs/architecture/lab-overview.md).
3. Follow [host workstation setup](docs/setup/workstation.md).
4. Configure [kubeconfig access](docs/setup/kubeconfig.md).
5. Use [the learning workflow](docs/workflow.md).

## Repository principles

- Commit working examples and their documentation together.
- Record prerequisites, commands, expected output, validation, cleanup, and troubleshooting.
- Never commit credentials, kubeconfig files, private keys, tokens, secrets, or sensitive Terraform state.
- Keep environment-specific values in local ignored files or secret managers.
- Mark untested commands and assumptions clearly.

## Status

Initial documentation scaffold. Host connectivity and kubeconfig authentication are **not yet verified** in this repository. Complete the setup steps from the host and record results in a sanitized form.

## License

No license has been selected yet. Until one is added, all rights are reserved by default.
