# Configure a cluster
kubectl create ns elasticstack
kubectl apply -f elasticsearch.yaml
kubectl apply -f kibana.yaml


kubectl port-forward -n elasticstack service/kibana 5601

kubectl delete ns elasticstack