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
