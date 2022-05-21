# Argo CD

Manage Kubernetes with [Argo CD](https://argo-cd.readthedocs.io/en/stable/)

With argocd CLI

Deploy an application:

```bash
kubectl apply -f application.yaml`
```


Create an App of Apps with the commands:

```bash
argocd app create apps \
--dest-namespace default \
--dest-server https://kubernetes.default.svc \
--repo https://github.com/st3w4r/argocd-apps.git \
--path apps

argocd app sync apps
```
