# Sysdig

<img src="../images/14.png" alt="drawing" width="250"/>

Make sure to store the incident file on the cluster's worker node.



```shell
# sysdig
sysdig -l |grep -iE 'time|user|proc'

# get tomcat id
docker ps|grep tomcat

# node
sysdig -M 30 -p "%evt.time,%user.uid,%proc.name" container.id=[container_id] > /opt/KSRS00101/incidents/summary
```