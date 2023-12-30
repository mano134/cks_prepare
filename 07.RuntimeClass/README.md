# Runtime Class

<img src="../images/7.png" alt="drawing" width="350"/>

## Runtime Class
```yaml
apiVersion: node.k8s.io/v1
kind: RuntimeClass
metadata:
  name: untrusted
handler: runsc
```
## Pod Runtime Class (handler)
```shell
kubectl get all -n server
```

```yaml
spec:
  runtimeClassName: untrusted   
  containers:
```