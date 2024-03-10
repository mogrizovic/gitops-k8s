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
