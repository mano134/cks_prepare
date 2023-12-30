## 14. Admission

```bash
# context
kubeadm was used to create the cluster used in this task.
# Task
Reconfigure and restart the cluster Kubernetes APl server to ensure that only authenticated and authorized REST requests are allowed.
authorization-mode=Node,RBAC admission-plugins=NodeRestriction
Delete ClusterRoleBinding of user system:anonymous

# Prepare
$ kubectl config use-context KSCH00101
# Answer
$ ssh ksch00101-master
$ vim /etc/kubernetes/manifests/kube-apiserver.yaml
- --authorization-mode=Node,RBAC
- --enable-admission-plugins=NodeRestriction
$ systemctl restart kubelet
$ kubectl delete clusterrolebinding system:anonymous
$ exit
```