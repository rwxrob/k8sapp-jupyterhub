# K8SAPP: JupyterHub

Add the Helm repo.

```
helm repo add jhub https://jupyterhub.github.io/helm-chart
helm repo update
```

Download the latest Helm chart tarball.

```
mkdir helm
cd helm
helm pull jhub/jupyterhub
```

Download `index.yaml` for later detection of new releases later.

```
curl -sSLO https://jupyterhub.github.io/helm-chart/index.yaml
```

Write the default resources to YAML file.

```
helm template jhub jupyterhub-1.2.0.tgz > jhub.yaml
```

Optionally, create local cluster for testing.

```
minikube start -p jhub
```

Create `jhub` namespace and set as current context. 

```
kubectl create ns jhub
k config set-context --current --namespace jhub
```

Install `jhub` with all the defaults just to test functionality.

```
kubectl apply -f jhub.yaml -n jhub
watch kubectl get po,no
```

Make custom configuration changes
