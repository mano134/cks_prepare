# Dockerfile Best Practices

doc：https://docs.docker.com/develop/develop-images/dockerfile_best-practices/

## Dockerfile
### 1、Dockerfile USER root
```shell
USER nobody
```
### 2、image check tag
```shell
FROM ubuntu:16.04
```


## Deployment
### 1、 change permission
```yaml
privileged: false
```
### 2、check apiVersion

```yaml
apiVersion: apps/v1
```

### 3、set id
```shell
runAsUser: 65535
readOnlyRootFilesystem': True,
```