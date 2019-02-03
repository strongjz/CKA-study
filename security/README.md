### [Security](./security/README.md)

1. Know how to configure authentication and authorization.
2. Understand Kubernetes security primitives.
3. Know to configure network policies.
4. Create and manage TLS certificates for cluster components.
5. Work with images securely.
6. Define security contexts.
7. Secure persistent key value store.
8. Work with role-based access control.

#### 1. Know how to configure authentication and authorization.

#####Authentication

https://v1-11.docs.kubernetes.io/docs/reference/access-authn-authz/authentication/

* Authentication Methods
* client certificates
* bearer tokens
* an authenticating proxy
* HTTP basic auth to authenticate API requests through authentication plugins

##### Authorization

https://v1-11.docs.kubernetes.io/docs/reference/access-authn-authz/authorization/

* Role - set of permissions that is namespaced
* RoleBinding - A role binding grants the permissions defined in a role to a user or set of users.
* ClusterRole - set of permissions that is cluster wide
* ClusterRoleBinding - DEFINE

High level: Cluster setup

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


https://www.youtube.com/watch?v=YRR-kZub0cA

