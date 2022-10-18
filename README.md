# Argocd Installation Guide & Vault Plugin Configuration (AVP)

1- Create namespace.

```bash
kubectl create namespace argocd
```
2- Apply rgocd manifests.

```bash
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```
