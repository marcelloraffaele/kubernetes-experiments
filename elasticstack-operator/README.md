# Intro
This is a test of deploy a ECK cluster on a local Kubernetes cluster.

I will follow this guide: https://www.elastic.co/guide/en/cloud-on-k8s/1.9/k8s-deploy-eck.html

# Installation
kubectl create -f https://download.elastic.co/downloads/eck/1.9.1/crds.yaml
kubectl apply -f https://download.elastic.co/downloads/eck/1.9.1/operator.yaml

check if everything went well:

kubectl -n elastic-system logs -f statefulset.apps/elastic-operator

# Configure a cluster
kubectl create ns eck
kubectl apply -f elasticsearch.yaml
kubectl apply -f kibana.yaml


## check the config
kubectl get elasticsearch -n eck
kubectl get kibana -n eck

kubectl port-forward -n eck service/quickstart-kb-http 5601


## clean
kubectl delete -f elasticsearch.yaml
kubectl delete -f kibana.yaml

kubectl delete -f https://download.elastic.co/downloads/eck/1.9.1/operator.yaml
kubectl delete -f https://download.elastic.co/downloads/eck/1.9.1/crds.yaml
kubectl delete ns eck