# Argocd Installation Guide & Vault Plugin Configuration (AVP)

1- Create namespace.

```bash
kubectl create namespace argocd
```
2- Apply rgocd manifests.

```bash
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

3- Download the [argocd-repo-server.yaml](https://github.com/mahafdah/argocd-installation-guide/blob/main/argocd-repo-server.yaml) file and execute bellow.

```bash
Kubectl patch deploy argocd-repo-server -n argocd --patch-file <your yml> # e.g. argocd-repo-server.yaml
```

```bash
Kubectl patch deploy argocd-repo-server -n argocd --patch-file argocd-repo-server.yaml
```
4- Download the [argocd-cm.yaml](https://github.com/mahafdah/argocd-installation-guide/blob/main/argocd-cm.yaml) configmap file and execute bellow.

```bash
Kubectl patch configmap argocd-cm -n argocd --patch-file <your yml> # e.g. argocd-cm.yaml
```

```bash
Kubectl patch configmap argocd-cm -n argocd --patch-file argocd-cm.yaml
```

5- We need to create a secret yaml file as bellow or you can download it from here [argocd-vault-plugin-credentials.yaml](https://github.com/mahafdah/argocd-installation-guide/blob/main/argocd-vault-plugin-credentials.yaml) but follow the Notes to know how to get the values in stringData.

```bash
apiVersion: v1
kind: Secret
metadata:
  name: argocd-vault-plugin-credentials ## Make sure this matches the same envFrom you put in the argocd-repo-server deployment
  namespace: argocd
type: Opaque
stringData:
  VAULT_ADDR: http://vault.vault:8200 ## Your vault address You can find this by running the command 'env' inside your vault pod and find VAULT_CLUSTER_ADDR=
  AVP_TYPE: vault
  AVP_AUTH_TYPE: approle
  AVP_ROLE_ID: role_id ## The role_id you copied earlier
  AVP_SECRET_ID: secret_id ## The secret_id you copied earlier
```

```bash
kubectl apply -f argocd-vault-plugin-credentials.yaml
```

Notes:
- The value of VAULT_ADDR if you are deploy the Vault & ARgocd in same cluster put the value as http:/<vault-svc-name>/<vault-namespace>:<svc port>
- The value of AVP_AUTH_TYPE & AVP_AUTH_TYPE keep as is.
- The value of AVP_ROLE_ID & AVP_SECRET_ID check the following [Dockument](https://github.com/mahafdah/vault-installation-guide) to know how get it.
  

















