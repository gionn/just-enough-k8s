# Install acs with helm

Allow nginx server snippets in annotations:

```sh
kubectl -n ingress-nginx patch cm ingress-nginx-controller \
  -p '{"data": {"allow-snippet-annotations":"true"}}'
```

Download the extra values for community version:

```sh
wget https://raw.githubusercontent.com/Alfresco/acs-deployment/master/helm/alfresco-content-services/community_values.yaml
```

Install:

```sh
helm install acs alfresco/alfresco-content-services \
  --values=community_values.yaml \
  --set global.search.sharedSecret=$(openssl rand -hex 24) \
  --atomic  --timeout 10m0s --namespace=alfresco
```
