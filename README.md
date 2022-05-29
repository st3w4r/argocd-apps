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
$ cat prod_config.yaml

apiVersion: kind.x-k8s.io/v1alpha4
networking:
        apiServerAddress: 192.168.0.1
        apiServerPort: 8444


$ kind create cluster --name prod --config prod_config.yaml

$ argocd cluster add kind-prod
```


Get access to the UI

- Port forward argo server
- Get password `kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo`
- Go to localhost:8080
- Username `admin`


Login if token as expired

```
sh ../password.sh

argocd login localhost:8080

> admin
> <password>

argocd cluster list
```



# Objective

- [ ] Multi cluster
- [ ] Folder with base application
- [ ] Deploy base app with custom configuration for each clsuter
- [ ] Manage ArgoCD by itself
- [ ] Automated test before env promotion


# ArgoCD manage itself

Based on: https://github.com/kurtburak/argocd


- Helm Chart: https://github.com/argoproj/argo-helm/tree/main/charts/argo-cd

```
$ kind create cluster --name argo

Creating cluster "argo" ...
 ✓ Ensuring node image (kindest/node:v1.21.1) 🖼
 ✓ Preparing nodes 📦
 ✓ Writing configuration 📜
 ✓ Starting control-plane 🕹️
 ✓ Installing CNI 🔌
 ✓ Installing StorageClass 💾
Set kubectl context to "kind-argo"
You can now use your cluster with:

kubectl cluster-info --context kind-argo

Not sure what to do next? 😅  Check out https://kind.sigs.k8s.io/docs/user/quick-start/

```

Change cotnext
```
$ kubectl config use-context kind-argo

Switched to context "kind-argo".

$ kubectl cluster-info - contact kind-argo

Kubernetes control plane is running at https://127.0.0.1:45119
CoreDNS is running at https://127.0.0.1:45119/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
```


Install helm chart
