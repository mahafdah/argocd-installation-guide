# Argocd Installation Guide & Vault Plugin Configuration (AVP)

1- Create namespace.

```bash
kubectl create namespace argocd
```
2- Apply rgocd manifests.

```bash
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

3- Download the [argocd-repo-server.yaml](https://github.com/mahafdah/argocd-installation-guide/blob/main/argocd-repo-server.yaml)file and execute bellow.

```bash
Kubectl patch deploy argocd-repo-server -n argocd --patch-file <your yml> # e.g. argocd-repo-server.yaml
```

```bash
Kubectl patch deploy argocd-repo-server -n argocd --patch-file argocd-repo-server.yaml
```
