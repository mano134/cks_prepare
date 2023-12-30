# Clusterrole
```bash
# context
A Role bound to a Pod serviceAccount grants overly permissive permissions.
Complete the following tasks to reduce the set of permissions.
# Task
Given an existing Pod named dev-pod running in the namespace monitoring.
Edit the existing Role bound to the Pod.
ServiceAccount service-account-web to only allow performing get operations, only on resources of type Pods.
Create a new Role named role-2 in the namespace monitoring, which only allows performing update operations, only on resources of type statefulsets.
Create a new RoleBinding named role-2-binding binding the newly created Role to the Pod ServiceAccount.
Don not delete the existing RoleBinding.
Note: Don't delete the existing RoleBinding.
```

```sh
# Prepare
$ kubectl config use-context KSTR00103
# Answer
$ kubectl get role -n monitoring 
NAME       CREATED AT
web-role   2021-12-17T09:30:05Z

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
```  
```sh
$ kubectl create role role-2 -n monitoring --verb=update --resource=statefulsets
$ kubectl create rolebinding role-2-binding -n monitoring --role role-2 --serviceaccount monitoring:service-account-web
```