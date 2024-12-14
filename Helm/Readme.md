```bash

helm install wordpress
helm upgrade wordpress
helm rollback wordpress
helm uninstall wordpress
# Helm search. Community Drive repository
helm search hub wordpress
```

```bash
hello-world-chart

templates
values
Charts
LICENCE
README.md
charts
```

# helm repo add

helm repo --help
helm repo add bitnami https://charts.bitnami.com/bitnami

# he

helm search repo wordpress
helm search hub wordpress

# Add a Chart repository

helm repo add

# Generate an index file given a directory containing packed charts

helm repo index

# List Chart Repositories

helm repo list

# Remove one or more repositories

helm repo remove

# Update information of available chart locally from Charts repositories

```bash
helm repo update

```

## Helm Commands

```bash
# List all existing releases
helm list
helm list -A

# Remove all kubernetes objects
helm uninstall my-release

helm pull --untar bitnami/wordpress
ls wordpress
helm install release-4 ./wordpress


helm pull bitnami/wordpress

helm pull --untar bitnami/wordpress

ls wordpresss

helm install my-release ./wordpress

helm search repo bitnami | grep apache

helm history nginx-release

helm rollback nginx-release 1
```

helm lint
helm template
helm --dry-run

## Managing Kubernetes with Helm

Creating a basic Helm chart

```bash
helm create mychart
# Check
ls -R
```

Download a Helm chart from a repository

```bash
helm pull [chart URL | repo/chartname] [...] [flags] ## this would download a helm, not install
helm pull --untar [rep/chartname] # untar the chart after downloading it
```

- To list all of the releases in the test-apps-apd

```bash
helm ls -n test-apps-apd
```

- Uninstall a application running in namespace

```bash
helm uninstall -n testing-apd image-scanner
```
