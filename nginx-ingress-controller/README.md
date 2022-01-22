# Intro
This experiment is based on OpenSource release of [NGINX Ingress Controller](https://kubernetes.github.io/ingress-nginx/).

# Ingress Controller Installation
As suggested by the [documentation](https://kubernetes.github.io/ingress-nginx/deploy/#quick-start) I Install using the deploy script:

```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.1.1/deploy/static/provider/cloud/deploy.yaml --validate=false
```




# Clean up
After the test if you want to clean, you can delete all the resources we have created during installation:
```
kubectl delete -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.1.1/deploy/static/provider/cloud/deploy.yaml
```


