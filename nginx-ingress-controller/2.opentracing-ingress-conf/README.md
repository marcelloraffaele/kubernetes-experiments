# Preconditions
The NGINX Ingress Controller must be installed

# Install Zipkin

```
kubectl apply -f zipkin.yaml
```

# Config Ingress Controller
We must modify the Ingress controller Config map adding:

```
data:
  enable-opentracing: "true"
  zipkin-collector-host: zipkin.zipkin.svc.cluster.local
```

we can do it using the command:

```
kubectl edit cm -n ingress-nginx ingress-nginx-controller
```

# Installation demo applications

```

kubectl apply -f app1.yaml
kubectl apply -f app2.yaml
```

# Test
```
curl -k http://demo.localdev.me/app1
curl -k http://demo.localdev.me/app2

```


# Clean up
```
kubectl delete namespace app1
kubectl delete namespace app2
kubectl delete namespace zipkin
```
