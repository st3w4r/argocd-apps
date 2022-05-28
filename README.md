# Argo CD

Manage Kubernetes with [Argo CD](https://argo-cd.readthedocs.io/en/stable/)

With argocd CLI

Create an App of Apps with the commands:

```bash
argocd app create apps \
--dest-namespace default \
--dest-server https://kubernetes.default.svc \
--repo https://github.com/st3w4r/argocd-apps.git \
--path apps

argocd app sync apps
```


Deploy the  application with kubectl:

```bash
# Create the app of Apps
kubectl apply -f applications.yaml

# Delete the app of Apps
kubectl delete -f applications.yaml
```

Create cluster

```
cat prod_config.yaml
| 
| apiVersion: kind.x-k8s.io/v1alpha4
| networking:
|         apiServerAddress: 192.168.0.1
|         apiServerPort: 8444
| 

kind create cluster --name prod --config prod_config.yaml

argocd cluster add kind-prod
```


Get access to the UI

- Port forward argo server
- Get password `kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo`
- Go to localhost:8080
- Username `admin`

