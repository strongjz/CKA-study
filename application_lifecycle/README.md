
## Application Lifecycle

* Understand Deployments and how to perform rolling updates and rollbacks.

[Kubernetes.io Deployment Documentation](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)


Deployment

This deployment will deploy 3 pods with container image NGINX 1.7.9 


```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.9
        ports:
        - containerPort: 80
```

```bash
kubectl apply -f deployment.yml

kubectl get deployments -l nginx
```


Rolling updates

--record will You may specify the --record flag to write the command executed in the resource annotation kubernetes.io/change-cause. It is useful for future introspection, for example to see the commands executed in each Deployment revision.

```bash
kubectl --record deployment.apps/nginx-deployment set image deployment.v1.apps/nginx-deployment
```





Rollbacks
```bash
```



* Know various ways to configure applications.


* Know how to scale applications.

```bash
```

* Understand the primitives necessary to create a self-healing application.

Primitives for Self Healing

* Deployment
* ReplicaSet
* Service
* Pods


```bash
```

