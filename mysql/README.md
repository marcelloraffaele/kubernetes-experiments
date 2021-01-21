# kubernetes-experiments: MySQL with persistent volume

This example shows how to create a MySQL Database in Kubernetes with persistent storage.
This means that data will be stored using persiste storage and every time the pod is deleted the data will restored.


From the documentation:
On-disk files in a container are ephemeral, which presents some problems for non-trivial applications when running in containers. 
from ([https://kubernetes.io/docs/concepts/storage/volumes/](https://kubernetes.io/docs/concepts/storage/volumes/))

This means that if we start a pod without specifying volumes it works till the pod will be destroyed and we will lose pur data.

In this example is created:
- A Secret for password management
- A Config map for initial SQL setup:
    - create user event db
    - create the 'event' table
    - insert some example rows in 'event' table
- A ReplicaSet for the singleton MySQL database instance that will use the secret and config map
- All the created objects have the "project=mysql-test" label, we can use it to identify the objects and manage it.

We are ready to create it:

```bash
cd mysql

kubectl apply -f mysql-configmap.yaml
kubectl apply -f mysql-secret.yaml
kubectl apply -f mysql-pvc.yaml
kubectl apply -f mysql-replicaset.yaml

#check
kubectl get configmap,secret,rs,pod,pvc,pv -l "project=mysql-test"
```
And the response will be something similar to this:
```bash
#this are the created objects
NAME                        DATA   AGE
configmap/mysql-configmap   1      7s

NAME                  TYPE     DATA   AGE
secret/mysql-secret   Opaque   2      7s

NAME                    DESIRED   CURRENT   READY   AGE
replicaset.apps/mysql   1         1         1       5s

NAME              READY   STATUS    RESTARTS   AGE
pod/mysql-d9g9t   1/1     Running   0          5s

```

Let's inspect the pod from inside:

```bash
#inspect the logs
kubectl logs {PODNAME}

#access the pod using bash
kubectl exec --stdin --tty {PODNAME} -- /bin/bash

#open mysql using root account
mysql -h localhost -u root -p
# write the 'root' password

#otherwise open mysql using root account
mysql -h localhost -u eventdb -p
# write the 'eventdb' password
```
Now that we have the mysql client running, we can check the database:
```bash
use eventdb;
SHOW TABLES;
select * from event;

mysql> delete from event where id=5;
Query OK, 1 row affected (0.02 sec)
mysql> commit;

quit
```

# Clean up
To clean everything we can use the label that we defined.
```bash
kubectl delete replicaset,configmap,secret,pvc -l "project=mysql-test"
```
As result we will see:
```bash
replicaset.apps "mysql" deleted
configmap "mysql-configmap" deleted
secret "mysql-secret" deleted
```