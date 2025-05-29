### Install Argocd Using Helm

```bash
helm install argocd argo/argo-cd -n argocd -f argo-cd/values.yml
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```
