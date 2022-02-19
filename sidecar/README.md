# Sidecar test
I deployed a sidecar container that can read the main container logs.

kubectl apply -f app.yaml
kubectl port-forward -n app1 service/app1 8080:80

