# AppArmor

<img src="../images/5.png" alt="drawing" width="300"/>

## doc：https://kubernetes.io/docs/tutorials/security/apparmor/


## enforce apparmor profile

```shell
ssh kssh00401-worker1

apparmor_parser -q /etc/apparmor.d/nginx_apparmor

apparmor_status | grep nginx
```

## prepare pod

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: hello-apparmor
  annotations:
    container.apparmor.security.beta.kubernetes.io/hello: localhost/nginx_apparmor
spec:
  containers:
  - name: hello
    image: busybox:1.28
    command: [ "sh", "-c", "echo 'Hello AppArmor!' && sleep 1h" ]
```