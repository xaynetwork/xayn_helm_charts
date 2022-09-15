# Quick Docker

Creeate a docker with https in the xayn-infrastructure

### Create values.yaml

```yaml
host: discovery-web-test-helm.xayn.com
container:
  image: xaynetci/xayn_discovery_web_service:zdf
  port: 3000
  secrets:
    - name: password
      value: ${SOME_ENV}
```

### Add the repo

```bash
helm repo add xayn https://xaynetwork.github.io/xayn_helm_charts/
```

### Render the 

If you used `${SOME_ENV}` variables you need to first replace / render them before using this helm chart:

```bash
export SOME_ENV=$GH_SECRET # 
envsubst < values.yaml | helm upgrade --install -f - --namespace <your-namespace> <your-deployment-name> 
```

and if not just do

```bash
cat values.yaml | helm upgrade --install -f - --namespace <your-namespace> <your-deployment-name> 
```