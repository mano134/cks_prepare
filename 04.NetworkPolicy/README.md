# Network Policy

<img src="../images/4.png" alt="drawing" width="250"/>

doc：https://kubernetes.io/docs/concepts/services-networking/network-policies/

```yaml
---
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: denypolicy
  namespace: testing
spec:
  podSelector: {}
  policyTypes:
  - Egress
  - Ingress
```

```sh
kubectl get ns qa --show-labels
kubectl get po products-service -n development --show-labels
```

![4-1](../images/4-1.png)
```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: pod-access
  namespace: development
spec:
  podSelector:
    matchLabels:
      role: pod-xxx # pod label
  policyTypes:
    - Ingress
  ingress:
    - from:
      - namespaceSelector:
          matchLabels:
            role: test # testing namespace label
    - from:
      - namespaceSelector: {} # namespace
        podSelector:
          matchLabels:
            enviroment: staging
```

```
root@k8s-master:~/cks# kubectl apply -f network-policy.yaml
```
