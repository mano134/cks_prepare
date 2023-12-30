# ImagePolicyWebhook

<img src="../images/1.png" alt="drawing" width="250"/>

## <font color=red>master node</font>
```sh
vim /etc/kubernetes/epconfig/kubeconfig
```
```yaml
clusters:
- cluster:
    certificate-authority: /etc/kubernetes/epconfig/external-cert.pem  # CA for verifying the remote service.
    server: https://acme.local:8082/image_policy # URL of remote service to query. Must use 'https'.
  name: image-checker
```
addmision_configration.yaml - zmien ustawienie
```yaml
defaultAllow: true -> false
```
vim /etc/kubernetes/manifests/kube-apiserver.yaml
```yaml
--enable-addmision-plugins=NodeRestriction,ImagePolicyWebhook
--addmision-control-config-file=/etc/kubernetes/epconfig/addmision_configuration.yaml
```
sprawdz czy jest zamontowany (powinien być)
```yaml
# mount
    volumeMounts:
    - mountPath: /etc/kubernetes/epconfig
      name: epconfig
# volumes      
  volumes:
    - name: epconfig
    	hostPath:
      	path: /etc/kubernetes/epconfig
```
```sh
systemctl daemon-reload
systemctl restart kubelet
```
## https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/#imagepolicywebhook
