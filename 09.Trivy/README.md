# Trivy

<img src="../images/9.png" alt="drawing" width="250"/>


```shell
# master
kubectl -n kamino get po -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.spec.containers[*].image}{"\n"}{end}'
# or
kubectl get pods --namespace kamino --output=custom-columns="NAME:.metadata.name,IMAGE:.spec.containers[*].image"
# or
kubectl get po -n kamino -oyaml | grep image:
```

```shell
# master
trivy image -s Critical,High pod-image
#or
trivy nginx | grep -E "HIGH|CRITICAL"
```

```shell
# delete vun pods
kubectl delete po xxx
```