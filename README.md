To create. First create namespace.

```
kubectl apply -f https://raw.githubusercontent.com/GrahamDumpleton/jupyter-on-kubernetes/master/namespace.yaml
```

Next deploy JupyterHub.

```
kubectl kustomize . | CLUSTER_SUBDOMAIN=A.B.C.D.nip.io envsubst '$CLUSTER_SUBDOMAIN' | kubectl apply -f -
```

In the above command replace ``A.B.C.D.nip.io`` with your ingress domain
for the Kubernetes cluster.

Get hostname to access JupyterHub by running:

```
kubectl get ingress -n jupyterhub-test1
```

When prompted for username/password, use anything for username, as it is
just a identifier for you. For password supply 'jupyterhub'.

To delete:

```
kubectl kustomize github.com/GrahamDumpleton/jupyter-on-kubernetes | CLUSTER_SUBDOMAIN=A.B.C.D.nip.io envsubst '$CLUSTER_SUBDOMAIN' | kubectl delete -f -
```

and:

```
kubectl delete -f https://raw.githubusercontent.com/GrahamDumpleton/jupyter-on-kubernetes/master/namespace.yaml
```
