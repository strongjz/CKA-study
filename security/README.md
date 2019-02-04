### [Security](./security/README.md)

1. Know how to configure authentication and authorization.
2. Understand Kubernetes security primitives.
3. Know to configure network policies.
4. Create and manage TLS certificates for cluster components.
5. Work with images securely.
6. Define security contexts.
7. Secure persistent key value store.
8. Work with role-based access control.

[Security Best practices Kubernetes deployment](https://kubernetes.io/blog/2016/08/security-best-practices-kubernetes-deployment/)

[Securing a kubernetes cluster](https://kubernetes.io/docs/tasks/administer-cluster/securing-a-cluster/)

[Building for Trust: How to Secure Your Kubernetes Cluster [I] - Alexander Mohr & Jess Frazelle](https://www.youtube.com/watch?v=YRR-kZub0cA)


#### 1. Know how to configure authentication and authorization.

##### Authentication

[AuthN AuthZ](https://docs.kubernetes.io/docs/reference/access-authn-authz/authentication/)

[RBAC](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

Authentication Methods
* client certificates
* bearer tokens
* an authenticating proxy
* HTTP basic auth to authenticate API requests through authentication plugins

##### Authorization


* Role - set of permissions that is namespaced
* RoleBinding - A role binding grants the permissions defined in a role to a user or set of users.
* ClusterRole - set of permissions that is cluster wide
* ClusterRoleBinding - A Cluster binding grants the permissions defined in a  clusterrole to a user or set of users.

#### 2. Understand Kubernetes security primitives.

Pod Security Policies

Network Policies

Resource Qoutas

PodSecurityContext->runAsNonRoot

https://kubernetes.io/docs/tasks/configure-pod-container/security-context/


Know how to configure authentication and authorization

    Access the api
    Authentication
    Authorization with RBAC
    Admission Control




#### 3. Know to configure network policies.



#### 4. Create and manage TLS certificates for cluster components.

https://kubernetes.io/docs/setup/certificates/
https://kubernetes.io/docs/reference/command-line-tools-reference/kubelet-tls-bootstrapping/


Kubernetes requires PKI for the following operations:

    Client certificates for the kubelet to authenticate to the API server
    Server certificate for the API server endpoint
    Client certificates for administrators of the cluster to authenticate to the API server
    Client certificates for the API server to talk to the kubelets
    Client certificate for the API server to talk to etcd
    Client certificate/kubeconfig for the controller manager to talk to the API server
    Client certificate/kubeconfig for the scheduler to talk to the API server.
    Client and server certificates for the front-proxy
    

#### High level: Cluster setup

https://kubernetes.io/docs/concepts/cluster-administration/certificates/

https://kubernetes.io/docs/tasks/tls/managing-tls-in-a-cluster/

A. Generating Certificates

1. Generate the CA configuration file, certificate, and private key
2. Generate a certificate and private key for each Kubernetes worker node:
3. Generate the kube-controller-manager client certificate and private key
4. Generate the kube-proxy client certificate and private key
5. Generate the kube-scheduler client certificate and private key
6. Generate the Kubernetes API Server certificate and private key
7. Generate the service-account certificate and private key
8. Copy the appropriate certificates and private keys to each worker instance
9. Copy the appropriate certificates and private keys to each controller instance

B. Generate Kube configs

1. Generate kubeconfig files for the controller manager, kubelet, kube-proxy, and scheduler clients and the admin user
2. Generate a kubeconfig file for each worker node
3. Generate a kubeconfig file for the kube-proxy service3
4. Generate a kubeconfig file for the kube-controller-manager service
5. Generate a kubeconfig file for the kube-scheduler service
6. Generate a kubeconfig file for the admin user
7. Copy the appropriate kubelet and kube-proxy kubeconfig files to each worker instance
8. Copy the appropriate kube-controller-manager and kube-scheduler kubeconfig files to each controller instance


#### 5. Work with images securely.

1. Scan images for CVE's
2. Run only authorized images
3. Sign container images
4. Run containers as non-root, non-privileged users

#### 6. Define security contexts.

#### 7. Secure persistent key value store.

How to Deploy a secure ETCD cluster

https://pcocc.readthedocs.io/en/latest/deps/etcd-production.html

https://coreos.com/os/docs/latest/generate-self-signed-certificates.html

https://coreos.com/etcd/docs/latest/op-guide/recovery.html

https://coreos.com/etcd/docs/latest/op-guide/configuration.html



#### 8. Work with role-based access control.



