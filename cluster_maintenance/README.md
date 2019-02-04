### [Cluster Maintenance](./cluster_maintenance/README.md)
1. Understand Kubernetes cluster upgrade process.


2. Facilitate operating system upgrades.


3. Implement backup and restore methodologies.


#### 1. Understand Kubernetes cluster upgrade process.

#### 2. Facilitate operating system upgrades.

#### 3. Implement backup and restore methodologies.

Vagrant create CoreOS Etcd cluster
https://github.com/strongjz/coreos-vagrant
http://www.adaltas.com/en/2018/06/20/coreos-dev-cluster-virtualbox/

```bash
ETCDCTL_API=3 etcdctl --endpoints $ENDPOINT snapshot save snapshotdb
# exit 0
# verify the snapshot
ETCDCTL_API=3 etcdctl --write-out=table snapshot status snapshotdb
+----------+----------+------------+------------+
|   HASH   | REVISION | TOTAL KEYS | TOTAL SIZE |
+----------+----------+------------+------------+
| fe01cf57 |       10 |          7 | 2.1 MB     |
+----------+----------+------------+------------+
```