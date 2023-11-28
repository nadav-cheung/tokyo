minikube addons enable metrics-server


手动
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
设置tls


kubectl apply -f components.yaml  