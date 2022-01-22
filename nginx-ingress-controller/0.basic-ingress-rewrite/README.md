# Preconditions
The NGINX Ingress Controller must be installed

# Installation

```
kubectl apply -f .\app1.yaml
kubectl apply -f .\app2.yaml
```

# Test
```
curl http://demo.localdev.me/app1
curl http://demo.localdev.me/app2
```


# Clean up
```
kubectl delete -f .\app1.yaml
kubectl delete -f .\app2.yaml
```
