## SealedSecrets

Install and use sealed secrets operator


### Installation



### Usage

Generate a normal secret

```bash
oc create secret generic mysecret --dry-run='client' -ojson  --from-literal=password=mypassword | kubeseal --controller-namespace sealed-secrets > mysealedsecret.json
```

Generate a sealed secret from the normal secret
```bash
kubeseal --controller-namespace sealed-secrets <mysecret.json >mysealedsecret.json
```

Add the secret to your project and visualize it
```
oc create -f mysealedsecret.json
oc get secret mysecret -o yaml
```
