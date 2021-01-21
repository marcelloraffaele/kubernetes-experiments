# kubernetes-experiments: prometeus
In this example I will show how to configure a Prometheus inside kubernetes.


```bash
kubectl apply -f prom-configmap.yaml
kubectl apply -f prom-deployment.yaml
kubectl get pod
kubectl port-forward service/prometheus 9090:9090

```

If we want to inspect:
kubectl describe cm prom-configmap


Create the example app:
kubectl apply -f starevent-event-app.yml
kubectl port-forward service/starevent-event 8081

service/starevent-event created
deployment.apps/starevent-event created

kubectl exec --stdin --tty {PODNAME} -- /bin/bash

## scale up the application
PS C:\Users\rmarc> kubectl scale deployment/starevent-event --replicas=5
deployment.apps/starevent-event scaled
PS C:\Users\rmarc> kubectl get deployment
NAME              READY   UP-TO-DATE   AVAILABLE   AGE
prometheus        1/1     1            1           3m32s
starevent-event   0/5     5            0           47m

# clean up

kubectl delete -f prom-deployment.yaml
kubectl delete -f prom-configmap.yaml

kubectl delete -f .\starevent-event-app.yml


more info on: https://prometheus.io/docs/prometheus/latest/configuration/configuration/#kubernetes_sd_config

https://github.com/prometheus/prometheus/blob/release-2.24/documentation/examples/prometheus-kubernetes.yml