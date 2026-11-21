# Secrets and Sensitive Data Policy

This repository is intended to be public reference material. Assume every committed file is visible to anyone.

## Never commit

- kubeconfig files, including `~/.kube/config` and `/etc/kubernetes/admin.conf`
- passwords, API tokens, bearer tokens, access keys, client secrets, or session cookies
- SSH private keys, TLS private keys, or credential bundles
- live Kubernetes Secret values or base64-encoded secret data (base64 is not encryption)
- cloud provider credential files
- Terraform state, local variable files containing sensitive values, or plan files that may embed secrets
- logs, command output, screenshots, or support bundles that expose credentials or private information

## Safe patterns

- Use placeholders in examples, such as `REPLACE_ME` or `<your-token>`.
- Commit `.env.example` only when it contains dummy values and no real secrets.
- Keep real configuration in ignored local files or use a secrets manager / approved CI secret store.
- Prefer Kubernetes Secret references and external secret-management integrations; never check in populated secret manifests.
- Review changes before pushing:

```bash
git status --short
git diff --check
git diff --cached
```

For an extra local check, scan staged files with a secret scanner (for example, Gitleaks) before committing.

## Important: .gitignore is not retroactive

Ignore rules prevent untracked matching files from being added. They do **not** remove files already tracked or erase secrets from Git history. If a secret is exposed:

1. Revoke or rotate it immediately.
2. Remove it from the current repository contents.
3. Treat it as compromised even if the commit is later amended or history rewritten.
4. Follow GitHub's sensitive-data removal guidance if history cleanup is required.

Do not paste secrets into issues, pull requests, chat, or terminal output while troubleshooting.
