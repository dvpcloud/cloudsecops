# Learning and Git Workflow

Use this workflow for each exercise so the repository remains useful as a reference and automation source.

1. Read the exercise and understand the security goal.
2. Inspect prerequisites and current cluster state.
3. Apply changes from the host workstation.
4. Validate behavior and capture sanitized output.
5. Add manifests, scripts, and notes to the repository.
6. Review for secrets and environment-specific assumptions.
7. Commit and push the completed work.

## Suggested commit messages

```text
docs: add host-based Kubernetes access guide
feat: add namespace-scoped RBAC exercise
security: add default-deny network policy example
automation: add validation script for lab prerequisites
```

## Exercise documentation template

Each exercise should explain:

- Objective and threat/security relevance
- Prerequisites
- Files and configuration
- Commands to run
- Expected results
- Validation and evidence
- Cleanup / rollback
- Troubleshooting
- Status: planned, in progress, tested, or needs review

## Git safety

Before pushing:

```bash
git status
git diff --check
git diff
```

Review staged changes for secrets. Never commit kubeconfig, SSH keys, tokens, passwords, secret manifests containing real values, or Terraform state with sensitive data.
