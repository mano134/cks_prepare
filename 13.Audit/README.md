# Audit

<img src="../images/13.png" alt="drawing" width="350"/>
## doc：https://kubernetes.io/docs/tasks/debug-application-cluster/audit/

## 1、enable audit (master node) 

```yaml
- --audit-policy-file=/etc/kubernetes/logpolicy/sample-policy.yaml
- --audit-log-path=/var/log/kubernetes/audit-logs.txt
- --audit-log-maxbackup=2 # The maximum number of old audit log files to retain. Setting a value of 0 will mean there's no restriction on the number of files.
- --audit-log-maxage=10 # The maximum number of days to retain old audit log files based on the timestamp encoded in their filename.
```

mount files: 

```yaml
...
volumeMounts:
  - mountPath: /etc/kubernetes/logpolicy/sample-policy.yaml
    name: audit
    readOnly: true
  - mountPath: /var/log/kubernetes/audit/
    name: audit-log
    readOnly: false
```

```yaml
...
volumes:
- name: audit
  hostPath:
    path: /etc/kubernetes/logpolicy/sample-policy.yaml
    type: File

- name: audit-log
  hostPath:
    path: /var/log/kubernetes/audit-logs.txt
    type: FileOrCreate
```

## 2. create policy
```yaml
apiVersion: audit.k8s.io/v1
kind: Policy
omitStages:
  - "RequestReceived"
rules:
  - level: RequestResponse
    resources:
    - group: ""
      resources: ["namespaces"]
  - level: Request
    resources:
    - group: ""
      resources: ["persistentvolumes"]
    namespaces: ["front-apps"]
  - level: Metadata
    resources:
    - group: ""
      resources: ["configmap", "secret"]
  - level: Metadata
    omitStages:
    - "RequestReceived"
```

## 3. restart kubelet
```shell
systemctl restart kubelet
```