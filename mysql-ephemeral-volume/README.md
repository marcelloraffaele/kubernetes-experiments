# kubernetes-experiments: MySQL Ephemeral volume

From the documentation:


On-disk files in a container are ephemeral, which presents some problems for non-trivial applications when running in containers. 
from ([https://kubernetes.io/docs/concepts/storage/volumes/](https://kubernetes.io/docs/concepts/storage/volumes/))

This means that if we start a pod without specifying volumes it works till the pod will be destroyed and we will lose pur data.



```bash
cd mysql-ephemeral-volume

kubectl apply -f mysql-configmap.yaml
kubectl apply -f mysql-replicaset.yaml

#check
kubectl get pod,rs,configmap -l "project=mysql-test"
```

Let's inspect the pod from inside:

```bash
kubectl logs {PODNAME}

kubectl exec --stdin --tty {PODNAME} -- /bin/bash
mysql -h localhost -u root -p
# write the root password



SELECT DATABASE();
SHOW TABLES;
```



# Clean up
```bash
kubectl delete -f mysql-replicaset.yaml
kubectl delete -f mysql-configmap.yaml
```