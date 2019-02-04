```bash
mkdir ~/bin
curl -s -L -o ~/bin/cfssl https://pkg.cfssl.org/R1.2/cfssl_linux-amd64
curl -s -L -o ~/bin/cfssljson https://pkg.cfssl.org/R1.2/cfssljson_linux-amd64
chmod +x ~/bin/{cfssl,cfssljson}
export PATH=$PATH:~/bin
mkdir ~/etcd-ca
cd ~/etcd-ca
echo '{"CN":"CA","key":{"algo":"rsa","size":2048}}' | cfssl gencert -initca - | cfssljson -bare ca -
echo '{"signing":{"default":{"expiry":"43800h","usages":["signing","key encipherment","server auth","client auth"]}}}' > ca-config.json
Server to Server Certs 
export NAME=node1
export ADDRESS=10.19.213.101,$NAME.mydomain.com,$NAME
echo '{"CN":"'$NAME'","hosts":[""],"key":{"algo":"rsa","size":2048}}' | cfssl gencert -config=ca-config.json -ca=ca.pem -ca-key=ca-key.pem -hostname="$ADDRESS" - | cfssljson -bare $NAME
scp ca.pem root@node1:/etc/etcd/etcd-ca.crt
scp node1.pem root@node1:/etc/etcd/server.crt
scp node1-key.pem root@node1:/etc/etcd/server.key
ssh root@node1 chmod 600 /etc/etcd/server.key
Config in /etc/etcd/etcd.conf
ETCD_NAME=node1
ETCD_LISTEN_PEER_URLS="https://10.19.213.101:2380"
ETCD_LISTEN_CLIENT_URLS="https://10.19.213.101:2379"
ETCD_INITIAL_CLUSTER_TOKEN="pcocc-etcd-cluster"
ETCD_INITIAL_CLUSTER="node1=https://node1.mydomain.com:2380,node2=https://node2.mydomain.com:2380,node3=https://node3.mydomain.com:2380"
ETCD_INITIAL_ADVERTISE_PEER_URLS="https://node1.mydomain.com:2380"
ETCD_ADVERTISE_CLIENT_URLS="https://node1.mydomain.com:2379"
ETCD_TRUSTED_CA_FILE=/etc/ssl/etcd/ca.pem
ETCD_CERT_FILE=“/etc/ssl/etcd/member.pem"
ETCD_KEY_FILE="/etc/ssl/etcd/member-key.pem"
ETCD_PEER_CLIENT_CERT_AUTH=true
ETCD_PEER_TRUSTED_CA_FILE=/etc/ssl/etcd/ca.pem
ETCD_PEER_KEY_FILE=/etc/ssl/etcd/member-key.pem
ETCD_PEER_CERT_FILE=/etc/ssl/etcd/client.pem
systemctl enable etcd
systemctl start etcd
 etcdctl —endpoints=https://node1.mydomain.com:2379 --ca-file=~/etcd-ca/ca.pem member list
ETCDCTL_API=3 ./etcdctl snapshot save snapshot.db —cacert /etc/ssl/etcd/ca.crt --cert /etc/ssl/etcd/client.crt --key /etc/ssl/etcd/client.key

etcd --name member1 --initial-advertise-peer-urls https://10.0.2.15:2380 \
  --listen-peer-urls https://10.0.2.15:2380 \
  --listen-client-urls https://10.0.2.15:2379,https://127.0.0.1:2379 \
  --advertise-client-urls https://10.0.2.15:2379 \
  --initial-cluster-token etcd-cluster-1 \
  --initial-cluster member1=https://10.0.2.15:2380 \
  --initial-cluster-state new \
  --client-cert-auth --trusted-ca-file=/etc/ssl/etcd/ca.pem \
  --cert-file=/etc/ssl/etcd/member1.pem --key-file=/etc/ssl/etcd/member1-key.pem \
  --peer-client-cert-auth --peer-trusted-ca-file=/etc/ssl/etcd/ca.pem \
  --peer-cert-file=/path/to/client.pem --peer-key-file=/etc/ssl/etcd/client-key.pem


ETCD_TRUSTED_CA_FILE="/etc/ssl/etcd/ca.pem"

ETCD_CERT_FILE="/etc/ssl/etcd/member.pem"

ETCD_KEY_FILE="/etc/ssl/etcd/member-key.pem"

ETCD_PEER_CLIENT_CERT_AUTH=true

ETCD_PEER_TRUSTED_CA_FILE="/etc/ssl/etcd/ca.pem"

ETCD_PEER_KEY_FILE="/etc/ssl/etcd/member-key.pem"

ETCD_PEER_CERT_FILE="/etc/ssl/etcd/client.pem"
```