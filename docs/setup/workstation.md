# Host Workstation Setup

This guide is for the host machine, not the `k8smaster` VM.

## 1. Create a local workspace

```bash
mkdir -p ~/projects
cd ~/projects
git clone https://github.com/dvpcloud/cloudsecops.git
cd cloudsecops
```

If you already cloned it, update:

```bash
git pull --ff-only
```

## 2. Check tools

```bash
git --version
kubectl version --client
```

Install kubectl using the official Kubernetes documentation for your operating system. Install Helm only when an exercise requires it.

## 3. Check host-to-master connectivity

```bash
ping -c 3 192.168.122.105
nc -vz 192.168.122.105 6443
```

A successful TCP check to port 6443 confirms network reachability, not successful authentication. If it fails, troubleshoot VM networking, routing, firewall rules, and API server listening address before proceeding.

## 4. Record results

Record date, host OS, kubectl client version, and sanitized connectivity results in the exercise notes. Do not publish local usernames, private IPs beyond what you intentionally disclose, credentials, or other sensitive infrastructure details in a public repo without reviewing them first.
