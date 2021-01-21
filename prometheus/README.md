# kubernetes-experiments: prometeus
In this example I will show how to configure a Prometheus inside kubernetes.


```bash
kubectl apply -f prometheus.yaml
kubectl apply -f grafana.yaml
```

If we want to inspect:
```bash
kubectl get pod,service,deployments,configmap -l "project=prom-test"
kubectl describe cm prom-configmap
kubectl describe cm grafana-configmap
```

If you want to open locally the prometheus console:
```bash
kubectl port-forward service/prometheus 9090:9090
```

If you want to open locally the grafana console:
```bash
kubectl port-forward service/grafana 3000:3000
```

Now that we have the environment ready we need an example app to monitor:

```bash
kubectl apply -f starevent-event-app.yml
kubectl port-forward service/starevent-event 8081:8081
```

## scale up the application
```bash
kubectl scale deployment/starevent-event --replicas=5
```

# clean up


```bash
kubectl delete -f prometheus.yaml
kubectl delete -f grafana.yaml

kubectl delete -f starevent-event-app.yml


```



more info on: https://prometheus.io/docs/prometheus/latest/configuration/configuration/#kubernetes_sd_config

https://github.com/prometheus/prometheus/blob/release-2.24/documentation/examples/prometheus-kubernetes.yml