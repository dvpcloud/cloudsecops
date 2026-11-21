# Kubeconfig and Host Authentication

kubectl reads cluster and authentication settings from kubeconfig, normally `~/.kube/config`. It uses the configured API endpoint and credentials to contact Kubernetes; routine kubectl commands do not require SSH.

## Bootstrap with kubeadm (administrator credential)

On a kubeadm control-plane node, the administrator kubeconfig is commonly `/etc/kubernetes/admin.conf`. It grants powerful cluster-admin access. Use it only as a secure bootstrap credential and never commit it.

From the host, if SSH access and permissions are configured:

```bash
mkdir -p ~/.kube
scp <ssh-user>@192.168.122.105:/etc/kubernetes/admin.conf ~/.kube/config
chmod 600 ~/.kube/config
```

If the SSH user cannot read the file, use a temporary copy on the master with restrictive permissions, transfer it, and remove the temporary copy immediately. Do not loosen permissions on the original file.

## Inspect and validate

```bash
kubectl config get-contexts
kubectl config view --minify
kubectl cluster-info
kubectl get nodes -o wide
kubectl get namespaces
```

Confirm the kubeconfig cluster server points to an address reachable from the host, for example:

```text
https://192.168.122.105:6443
```

Do not blindly change the cluster name in `kubectl config set-cluster`; first inspect the actual name in the current kubeconfig.

## Next: least privilege

After bootstrap access works, create a dedicated identity and RBAC role for the learning namespace. Use that identity for routine exercises instead of the administrator credential.

## Troubleshooting

- **Timeout / connection refused:** verify host routing, VM network mode, firewall, and API server port.
- **TLS certificate error:** ensure the API endpoint hostname/IP is covered by the API server certificate and the CA data is correct. Do not disable TLS verification as a workaround.
- **Unauthorized:** check credential validity and authentication configuration.
- **Forbidden:** authentication succeeded, but the identity lacks the requested RBAC permission.

## Secret handling

Never commit `~/.kube/config`, `admin.conf`, tokens, client private keys, or copied credential files. Keep them local with restrictive permissions and use secret scanning.
