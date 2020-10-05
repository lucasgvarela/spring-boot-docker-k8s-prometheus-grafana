To build the dockerfile
```
docker build . -t lucasgvarela2/hellovarela:v1
```

To pull my already created image from https://hub.docker.com/r/lucasgvarela2/hellovarela and run it in background
```
docker run -d --rm -p 8080:8080 lucasgvarela2/hellovarela:v1
```

To test
```
open http://localhost:8080 on your web browser
```

To deploy on k8s, this will create a deployment with 1 pod replica and 1 service type load balancer with port 80 exposed
```
kubectl apply -f k8s/
minikube tunnel
kubectl get svc # get the LoadBalancer example-service external IP and open on the browser
```

Prometheus + Grafana to monitor the application with actuator + micrometer-registry-prometheus for Spring Boot on pom.xml
```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo add stable https://kubernetes-charts.storage.googleapis.com/
helm repo update
helm install prom-test prometheus-community/kube-prometheus-stack
kubectl port-forward prom-test-grafana-$id 3000
kubectl get secrets prom-test-grafana -o jsonpath="{.data.admin-user}" | base64 --decode; echo
kubectl get secrets prom-test-grafana -o jsonpath="{.data.admin-password}" | base64 --decode; echo
kubectl port-forward prometheus-prom-test-kube-prometheus-prometheus-0 9090
```
