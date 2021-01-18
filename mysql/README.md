# kubernetes-experiments: MySQL


```bash
cd mysql
kubectl apply -f nfs-volume-claim.yaml
kubectl apply -f mysql-replicaset.yaml
```




```bash
kubectl get pvc -o wide
kubectl get volume
kubectl get rs
kubectl get pod

kubectl get pod,rs,pvc -l "project=mysql-test"
```

Let's inspect the pod from inside:

```bash
kubectl logs mysql-pjgts

kubectl exec --stdin --tty mysql-pjgts -- /bin/bash
mysql -h localhost -u root -p

SELECT DATABASE();
SHOW TABLES;
```

# Clean up
```bash
kubectl delete pod,rs,volume,pvc -l "project=mysql-test"
```