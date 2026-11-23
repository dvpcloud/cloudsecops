# Cloud SecOps Learning Path

A practical, version-controlled learning environment for Kubernetes, cloud security, DevSecOps automation, AI security and security operations.

## Authoritative project records

These three files are the canonical continuity records:

1. [Project state](PROJECT_STATE.md) — lab inventory, architecture decisions and operating constraints.
2. [Learning progress](LEARNING_PROGRESS.md) — verified learning, evaluations and milestone status.
3. [Next steps](NEXT_STEPS.md) — active exercise queue and immediate actions.

The six-month curriculum remains in [ROADMAP.md](ROADMAP.md).

## Lab approach

- **Host workstation:** source code, Git, kubectl, Helm, Terraform and security tools.
- **Kubernetes control plane:** existing `k8smaster` VM; not the primary project workstation.
- **Remote administration:** kubectl on the host communicates with the Kubernetes API over HTTPS using a protected kubeconfig.
- **GitHub:** canonical reference for tested manifests, scripts, notes, architecture and repeatable exercises.

## Repository principles

- Inspect existing files and current lab state before changes.
- Commit working examples and their documentation together.
- Record prerequisites, commands, expected output, validation, cleanup and troubleshooting.
- Never commit credentials, kubeconfig files, private keys, tokens, live Secret values or sensitive Terraform state.
- Keep environment-specific values in ignored local files or secret managers.
- Mark untested commands and assumptions clearly.
- Do not push changes without authorization; verify every authorized change.

## Existing documentation

- [Lab architecture](docs/architecture/lab-overview.md)
- [Host workstation setup](docs/setup/workstation.md)
- [Kubeconfig access](docs/setup/kubeconfig.md)
- [Learning workflow](docs/workflow.md)
- [Secrets and sensitive data policy](docs/security/secrets-handling.md)

## License

No license has been selected yet. Until one is added, all rights are reserved by default.
