## To Run on a Minikube Instance:

### Start Minikube
 `minikube start`

### Apply Kubernetes Manifests

##### Elasticsearch
```
kubectl apply -f Elasticsearch/Elastic-Namespace.yaml
kubectl apply -f Elasticsearch/Elastic-StatefulSet.yaml
kubectl apply -f Elasticsearch/Elastic-Service.yaml
curl -k "http://elasticsearch:9200"              # validate elastic health (from a pod)
```

##### Kibana
```
kubectl apply -f Kibana/Kibana-ConfigMap.yaml
kubectl apply -f Kibana/Kibana-Deploy.yaml
kubectl apply -f Kibana/Kibana-Service.yaml
minikube service kibana -n logging-system --url  # Get internal access to Kibana UI
```
##### Filebeat
```
kubectl apply -f Filebeat/Filebeat-RBAC.yaml
kubectl apply -f Filebeat/Filebeat-ConfigMap.yaml
kubectl apply -f Filebeat/Filebeat-DaemonSet.yaml
```

### Upload Hello World App
```
kubectl apply -f Application/App-ConfigMap.yaml
kubectl apply -f Application/App-Deploy.yaml
kubectl apply -f Application/App-Service.yaml
```

### Interact with App
```
kubectl port-forward svc/hello-world -n hello-world 8080:80   # port-forwarding (from host)
http://localhost:8080                                         # View html page (from browser)
```

### Cleanup
```
kubectl delete ns logging-system
minikube stop
```