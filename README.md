# openshift-gitops
Repo to install and configure openshift-gitops on OCP 4.7


## Authenticate with cluster admin creds

```bash
oc login -u cluster-admin-user https://your-api:6443
```

## Install operator

```bash
oc replace -f install-operator/gitops-op.yaml
oc apply -f install-operator/gitops-sb.yaml
```

## Get openshift-gitops GUI creds (AKA argocd-for-admins)

```bash
oc get secret openshift-gitops-cluster -n openshift-gitops -o jsonpath='{.data.admin\.password}' | base64 -d
```

## Deploy environment-definitions App

- This creates the argocd-for-developers project and projects that will be managed by it
- It also sets quotas, rolebindings, and any initial resource for the projects

```bash
oc apply -k https://github.com/manurodriguez/openshift-gitops/environment/openshift-gitops 
```

## Once the environments-definitions App is ready, create the argocd-for-developers App

```bash
oc apply -k https://github.com/manurodriguez/openshift-gitops/environment/argocd-for-developers
```

## Get developers openshift-gitops GUI (AKA argocd-for-developers)

```bash
oc get secret argocd-cluster -n argocd -o jsonpath='{.data.admin\.password}' | base64 -d
```
