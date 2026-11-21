# Lab Overview

## Architecture decision

Use the host as the DevSecOps workstation and keep the Kubernetes control-plane VM focused on operating the cluster.

```text
HOST WORKSTATION
  Git / editor / kubectl / Helm / Terraform / Ansible / security tools
             |
             | HTTPS Kubernetes API (TCP 6443)
             v
k8smaster — control plane
  API server / etcd / scheduler / controller manager
             |
             v
Kubernetes workloads
  devsecops-lab namespace and future exercises
```

## Known environment details

Project notes identify the control-plane node as `k8smaster`, with an internal IP of `192.168.122.105` and Kubernetes API port `6443`. This address must be reachable from the host and may be specific to the current virtualization/network configuration.

Previously observed cluster components include Argo CD, Calico, and Envoy Gateway. Confirm current status with kubectl before making changes.

## Workstation/control-plane separation

The host stores the working repository and runs client tools. Kubernetes commands use the API server; SSH is used only for host administration or initial secure credential transfer, not for every kubectl operation.

## Security boundaries

- Do not store administrator kubeconfig in this repository.
- Prefer a dedicated, least-privilege identity for daily exercises.
- Keep cluster bootstrap credentials offline or in an approved secure location.
- Use namespaces and RBAC to scope exercise access.
- Treat public repository contents as fully public.
