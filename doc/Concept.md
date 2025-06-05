# A comparative analysis of Minikube vs Kind vs K3d for deploying Kubernetes clusters locally.   

## Introduction
This document presents a comparative analysis of Minikube, Kind vs K3d for deploying Kubernetes clusters locally. The purpose of this is to select the most appropriate tool for a local kubernetes cluster. Create a PoC using a preffered tool.

## Tools

### Minikube

[Minikube](https://minikube.sigs.k8s.io/docs/) is a one-node Kubernetes cluster where master processes and work processes both run on one node. [[1](https://www.geeksforgeeks.org/kubernetes-minikube/)] According to the official documentation of Minikube, Minikube is local Kubernetes, focusing on making it easy to learn and develop for Kubernetes. [[2](https://minikube.sigs.k8s.io/docs/start/?arch=%2Fmacos%2Farm64%2Fstable%2Fbinary+download)]

### Kind (Kubernetes IN Docker)

[Kind](https://github.com/kubernetes-sigs/kind) is a tool for running local Kubernetes clusters using Docker container “nodes”.
kind was primarily designed for testing Kubernetes itself, but may be used for local development or CI. kind supports [docker](https://www.docker.com), [podman](https://podman.io) or [nerdctl](https://github.com/containerd/nerdctl) [[3](https://kind.sigs.k8s.io/)].

### K3d
[K3d](https://k3d.io/stable/) is a lightweight wrapper to run k3s (Rancher Lab’s minimal Kubernetes distribution) in docker. K3d makes it very easy to create single- and multi-node k3s clusters in docker, e.g. for local development on Kubernetes.

## Features

| Feature               | Minikube                                      | Kind                                       | K3d                                        |
|-----------------------|-----------------------------------------------|--------------------------------------------|--------------------------------------------|
| Purpose               | Local Kubernetes on VMs or bare metal         | Kubernetes clusters in Docker containers   | Local dev/test using K3s in Docker         |
| Host OS Compatibility | Linux, macOS(Docker/VM), Windows(Docker/WSL2) | Linux, macOS(Docker), Windows(Docker/WSL2) | Linux, macOS(Docker), Windows(Docker/WSL2) |
| Architecture          | amd64 / arm64 (limited)                       | amd64 / arm64                              | amd64 / arm64                              |
| Runs in               | VM or container (Docker/Podman)               | Docker containers                          | Docker containers                          |
| Dependencies          | VirtualBox, Hyperkit, Docker                  | Docker only                                | Docker only                                |
| Best For              | Local development                             | CI pipelines, local K8s testing            | CI pipelines, local K8s testing            |
| Multi-node Support    | Yes                                           | Yes                                        | Yes                                        |
| Monitoring            | Prometheus/Grafana via addons                 | Prometheus/Grafana via Helm                | Prometheus/Grafana via Helm                |
| Production Ready      | No (dev only)                                 | No (dev/CI only)                           | No (dev/CI only)                           |

## Pros and Cons

### Minikube

**Pros**
- Easy to set up.
- One of the fastest ways to spin up a local Kubernetes cluster.
- Great for beginners learning Kubernetes.
- Multi-Platform support (Windows, macOS, and Linux).
- Supports different virtualization backends: Docker, VirtualBox, KVM, Hyper-V, Podman etc.
- Supports Kubernetes add-ons like Ingress, Dashboard, Metrics Server.
- Supports multi-node clusters.

**Cons**
- Not ideal for team collaboration or shared environments.
- Can't scale beyond your machine's resources.
- Not meant for Production.
- Can be heavy on RAM and CPU if you’re running a complex cluster.
- Manual cluster management

### Kind
- Runs in Docker (no VM needed).
- Lightweight and fast startup, especially compared to Minikube with a VM driver.
- Great for CI/CD pipelines (e.g., GitHub Actions, GitLab CI).
- Easy to spin up multi-node clusters using a simple YAML config.
- Declarative cluster configuration, fully configurable via YAML files—cluster layout, node roles, container runtime settings, etc.
- Cross-platform support (Linux, macOS, and Windows (with Docker installed)).

**Cons**
- Docker/Podman required
- Ingress and port mapping can be more manual than Minikube.
- No Built-in dashboard or Add-ons (like Minikube's dashboard).

### K3d

**Pros**
- Lightweight and fast.
- Super quick to start and consumes fewer resources than Minikube or Kind.
- Easily creates multi-node clusters (including load balancer, server, and agent nodes).
- Docker-Based, no need for virtualization or VMs—runs entirely in Docker containers.
- Works well across platforms (Linux, macOS, Windows with Docker Desktop).
- Can automatically expose services via Traefik ingress (built-in to K3s).
- Supports containerd by default (same runtime used in many cloud environments).
- Works well with Helm, kubectl, and other cloud-native tools.

**Cons**
- Docker is reqquired.
- Some features (like cloud controller manager, dynamic volume provisioning) are simplified or removed.
- k3s behaves slightly differently than full Kubernetes (e.g., uses Traefik by default).
- Exposing ports or services outside Docker may require manual configuration.
- No built-in dashboard or web UI—you’ll have to install one yourself.

## Demo
![k3d demo](demo.gif)

## Conclusion

**K3d was chosen for its simplicity, fast setup, and strong alignment with local development needs.** Docker's licensing is not a limiting factor at this point, as the small two-person team qualifies for free usage. While Podman was considered for its rootless operation and systemd integration, its ecosystem is still maturing. Minikube, though powerful, demands more system resources and is less optimal for quick iteration. Kind excels in CI/CD environments but lacks the ease of use and interactivity desired for day-to-day local development.