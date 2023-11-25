# EVERYTHING GITOPS IN KUBERNETES
Local platform is MacOs

## 1. kind

Local kubernetes cluster with docker.
Cluster with config file provided, creates Ingress (nginx) enabled cluster.

Create a kind cluster with extraPortMappings and node-labels.

- `extraPortMappings` allow the local host to make requests to the Ingress controller over ports 80/443
- `node-labels` only allow the ingress controller to run on a specific node(s) matching the label selector.

### install

```sh
kind create cluster --name gitops-k8s --config ./kind/cluster-config.yaml
```

## 2. nginx

Kubernetes ingress controller.

### install

Installing kind specific installation
```sh
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml
```

## 3. argocd

ArgoCD installation.

### install

- create argocd ns
```sh
kubectl create namespace argocd
```
- install argocd with custom values
```sh
helm install argocd argo/argo-cd -n argocd -f ./argocd/values.yaml
```
- export generated password to `ARGOCD_PASS` env var
```sh
export ARGOCD_PASS=$(kubectl -n default get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d)
```