# Role/Rolebinding/Serviceaccunt

<img src="../images/16.png" alt="drawing" width="350"/>


## 修改 Role
```shell
$ kubectl edit role -n monitoring web-role 
```
```yaml
...
rules:
- apiGroups:
  - ""
  resources:
  - pods
  verbs:
  - get

#or
k create role role01 --resource=endpoints --verb get -n db
```

## create role
```
k create role role-2 --resource=namespaces --verb delete -n db
```

## create rolebinding
```shell
k create rolebinding role-2-binding --role role-2 --serviceaccount db:service-account-web
```