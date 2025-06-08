# PoC: Argo CD on K3d cluster

## Prerequisites

- Docker/podman
- curl/wget

## Download and install K3d

Official documentation https://k3d.io/stable/#releases

```bash
curl -s https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | bash
```

## Create a cluster with just a single server node

```bash
k3d cluster create argocd
```

## Install Argo CD

```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

Check state of the Argo CD pods

```bash
kubectl get pods -n argocd
```

## ArgoCD web access

Enable port-forwarding to access the Argo CD via a web browser

```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

Open in you web browser. By default Argo CD uses https protocol and self-signed certificates

```bash
https://localhost:8080
```

## Admin Password

```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```
