# Secrets

<img src="../images/3.png" alt="drawing" width="250"/>

# Prepare
$ kubectl config use-context KSMV00201
# Answer

```sh
$ kubectl get secrets -n monitoring db1-test -oyaml
```
```yaml
apiVersion: v1
data:
  password: cGFzcw==
  username: YWRtaW4=
...
```
```bash
$ echo "cGFzcw==" | base64 -d > /home/candidate/old-password.txt
$ echo "YWRtaW4=" | base64 -d > /home/candidate/user.txt

# or 
kubectl -n istio-system get secrets db1-test -ojsonpath='{.data.user}'|base64 -d > /etc/candidate/user.txt

kubectl -n istio-system get secrets db1-test -ojsonpath='{.data.pass}'|base64 -d > /etc/candidate/pass.txt

$ kubectl create secret generic dev-mark -n monitoring --from-literal=username=production-instance --from-literal=password=aVJdk7NSjk

$ vim secret-pod.yaml
```

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: secret-pod
  namespace: monitoring
spec:
  containers:
  - name: test-secret-container
    image: redis
#add
    volumeMounts:
    - name: secret-volume
      mountPath: "/etc/test-secret"
      readOnly: true
  volumes:
  - name: secret-volume
    secret:
      secretName: dev-mark
      optional: false
```
```
$ kubectl apply -f secret-pod.yaml
```
