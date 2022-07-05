# IBL Navigator

Deployments in this project have files split between multiple locations, to allow common files to be used by multiple deployments.
To apply or delete, run the following:

```bash
( export VISIBILITY=<private | public> && export SUBDOMAIN=<your deployment> && kubectl -n ibl-navigator-${SUBDOMAIN} <apply | delete> -f k8s/deployments/navigator-${VISIBILITY}/${SUBDOMAIN} -f k8s/deployments/navigator-${VISIBILITY}/ )
```

If an entierly new deployment needs to be made, complete the following:

- create a new subdirectory in the navigator directory: `mkdir navigator/<your deployment>`
- establish a new namespace: `kubectl create namespace ibl-navigator-<your deployment>`
- set a DNS record in gandi of type CNAME, with name = your deployment, and having a hostname identical to that of `data`
- configure deployment files in your subdirectory
- apply deployment with `( export VISIBILITY=<private | public> && export SUBDOMAIN=<your deployment> && kubectl -n ibl-navigator-${SUBDOMAIN} <apply | delete> -f navigator-${VISIBILITY}/${SUBDOMAIN} -f navigator-${VISIBILITY}/ )`

# Jupyterhub
install|update:
```bash
source k8s/deployments/jupyterhub/.env && helm upgrade --install jupyterhub jupyterhub/jupyterhub -n jhub --create-namespace --values k8s/deployments/jupyterhub/helm_config.yaml --set hub.config.GitHubOAuthenticator.client_id=${GITHUB_CLIENT_ID} --set hub.config.GitHubOAuthenticator.client_secret=${GITHUB_CLIENT_SECRET} --set hub.db.url=${JUPYTERHUB_DB_URL} --version "1.1.3" --devel --timeout 1h --debug #--wait --dry-run
```
remove:
```bash
helm delete jupyterhub -n jhub # && kubectl delete ns jupyterhub
```
note: deleting namespace is currently permanently breaking dns resolution for that ns (matching name)

