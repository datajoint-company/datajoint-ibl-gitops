Deployments in this project have files split between multiple locations, to allow common files to be used by multiple deployments.
To apply or delete, run the following:
```( export SUBDOMAIN=<your deployment> && kubectl -n ibl-navigator-${SUBDOMAIN} <apply | delete> -f navigator/${SUBDOMAIN} -f navigator/ )```

If an entierly new deployment needs to be made, complete the following:
- create a new subdirectory in the navigator directory: `mkdir navigator/<your deployment>`
- establish a new namespace: `kubectl create namespace ibl-navigator-data-<your deployment>`
- set a DNS record in gandi of type CNAME, with name = your deployment, and having a hostname identical to that of `data`
- configure deployment files in your subdirectory
- apply deployment with `( export SUBDOMAIN=<your deployment> && kubectl -n ibl-navigator-${SUBDOMAIN} <apply | delete> -f navigator/${SUBDOMAIN} -f navigator/ )`
