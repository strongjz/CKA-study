
## Application Lifecycle

1. Understand Deployments and how to perform rolling updates and rollbacks.
2. Know various ways to configure applications.
3. Know how to scale applications.
4. Understand the primitives necessary to create a self-healing application.

#### 1. Understand Deployments and how to perform rolling updates and rollbacks.

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

Send the deployment yaml to the api server
```bash
kubectl apply -f deployment.yml
```

This command will show the deployment status 
```bash
kubectl rollout status deployment.v1.apps/nginx-deployment
```

Retrieve information about deployment 
```bash
kubectl get deployments -l nginx
```


Retrieve all the information about deployment 
```bash
kubectl describe deployments nginx-deployment
```

```bash
kubectl get pods --show-labels -l nginx
```

Rolling updates

```monotone
--record flag to write the command executed in the resource annotation kubernetes.io/change-cause. It is useful for future introspection, for example to see the commands executed in each Deployment revision.

```

```bash
kubectl --record deployment.apps/nginx-deployment set image deployment.v1.apps/nginx-deployment
```



Rollbacks

Changing the image
```bash
kubectl set image deployment.v1.apps/nginx-deployment nginx=nginx:1.91 --record=true
```

Using History

```bash
kubectl rollout history deployment.v1.apps/nginx-deployment
```
```bash
REVISION    CHANGE-CAUSE
1           kubectl create --filename=https://k8s.io/examples/controllers/nginx-deployment.yaml --record=true
2           kubectl set image deployment.v1.apps/nginx-deployment nginx=nginx:1.9.1 --record=true
3           kubectl set image deployment.v1.apps/nginx-deployment nginx=nginx:1.91 --record=true
```

To get more information about a Revision
```bash
kubectl rollout history deployment.v1.apps/nginx-deployment --revision=2
```

You can update a deployment with a revision number
```bash
 kubectl rollout undo deployment.v1.apps/nginx-deployment --to-revision=2
```


#### 2.  Know various ways to configure applications.

   1. yaml - create yaml file like the one [here](./deployment.yml) 
    
   2. edit - edit a deployment that is already running, this command will pop up the deployment yaml in the default text editor.

   ```bash
   kubectl edit deployment.v1.apps/nginx-deployment
   ```

   3. run - kubectl run [generators](https://kubernetes.io/docs/reference/kubectl/conventions/#generators) allow you to use the kubectl cli directly to create objects 
    
   ```bash
   kubectl run nginx --image=nginx --replicas=5
   ```

#### 3. Know how to scale applications.

```bash
 kubectl scale deployment.v1.apps/nginx-deployment --replicas=10
```

#### 4. Understand the primitives necessary to create a self-healing application.

Service are a single virtual IP for the deployment, A deployment manages a replicaset, which deploys sets of pods.
A deployment with many replicas ensures the applications pods are still running in the event of a pod or node failure


Primitives for Self Healing
* [Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) - Manages replica sets
* [ReplicaSet](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/) - defines the current version and other app metadata
* [Service](https://kubernetes.io/docs/concepts/services-networking/service/) - Single entry point for application
* [Pods](https://kubernetes.io/docs/concepts/workloads/pods/pod/) - Collection of containers that run the application




