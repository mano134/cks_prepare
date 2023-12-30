# kube-bench

<img src="../images/10.png" alt="drawing" width="250"/>

## 0. master kube-bench

```shell
$ ssh kscs00201-master
$ kube-bench run node/master/etcd
```

## 1. api server (/etc/kubernetes/manifests/kube-apiserver.yaml) master
```yaml
- --authorization-mode=Node,RBAC
```

## 2. kubelet (/var/lib/kubelet/config.yaml) worker node
```yaml
apiVersion: kubelet.config.k8s.io/v1beta1
authentication:
  anonymous:
    enabled: false # set false
  webhook:
    cacheTTL: 2m0s
    enabled: true
  x509:
    clientCAFile: /etc/kubernetes/pki/ca.crt
authorization:
  mode: Webhook # set Webhook
  webhook:
    cacheAuthorizedTTL: 5m0s
    cacheUnauthorizedTTL: 30s
...
```

## 3. etcd.yaml (/etc/kubernetes/manifests/etcd.yaml )
```yaml
- --client-cert-auth=true
```

## 4. restart kubelet

```shell
service kubelet restart
```

