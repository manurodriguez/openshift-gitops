# openshift-gitops
Repo to install and configure openshift-gitops on OCP 4.7

## Install operator

```bash
oc replace -f install-operator/gitops-op.yaml
oc apply -f install-operator/gitops-sb.yaml
```
