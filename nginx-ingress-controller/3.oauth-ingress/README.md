# How to
https://github.com/kubernetes/ingress-nginx/tree/main/docs/examples/auth/oauth-external-auth
https://kubernetes.github.io/ingress-nginx/examples/auth/oauth-external-auth/

# Preconditions
The NGINX Ingress Controller must be installed

# Create certificates and secret
Let's think i want to protect the host: `secure.localdev.me`

We can create a simple self signed certificate that we could use ONLY FOR TEST using the following command:

```
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout mykey.key -out mycert.crt -subj "/CN=secure.localdev.me/O=secure.localdev.me"
```

# Installation

```
kubectl create namespace app1
kubectl create secret tls my-tls-cert --key mykey.key --cert mycert.crt --namespace app1
kubectl apply -f app.yaml

kubectl create namespace oauth2-proxy
kubectl create secret tls my-tls-cert --key mykey.key --cert mycert.crt --namespace oauth2-proxy
kubectl apply -f oauth2-proxy.yaml

kubectl apply -f ingress.yaml

```

# Test
```
curl -k https://secure.localdev.me

```


# Clean up
```
kubectl delete namespace app1
```
