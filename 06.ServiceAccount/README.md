# Service account
![6](../images/6.png)

doc: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/

## 1. create service account

### service account

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: backend-sa
  namespace： qa
automountServiceAccountToken: false #add
```

### pod
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
  namespace: qa 
spec:
  serviceAccountName: backend-sa
  automountServiceAccountToken: false #add
```

## 2. find and delete unused service accounts

```shell
kubectl get po -oyaml|grep -i serviceaccountname

kubectl get sa

kubectl delete sa XXX
```