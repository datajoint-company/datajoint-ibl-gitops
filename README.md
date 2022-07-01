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

# SciViz

Deployments in this project have files split between multiple locations, to allow common files to be used by multiple deployments.
To apply or delete, run the following:
```bash
( export VISIBILITY=<private | public> &&  kubectl -n sci-viz-${VISIBILITY} apply -f k8s/deployments/sciviz/hpa.yaml -f k8s/deployments/sciviz/secret.yaml -f k8s/deployments/sciviz/${VISIBILITY}/sci-viz/ -f k8s/deployments/sciviz/${VISIBILITY}/pharus/ )
```
