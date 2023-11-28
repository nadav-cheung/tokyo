kubectl apply -f https://github.com/kubesphere/ks-installer/releases/download/v3.3.2/kubesphere-installer.yaml
kubectl apply -f https://github.com/kubesphere/ks-installer/releases/download/v3.3.2/cluster-configuration.yaml


kubectl delete -f https://github.com/kubesphere/ks-installer/releases/download/v3.3.2/kubesphere-installer.yaml
kubectl delete -f https://github.com/kubesphere/ks-installer/releases/download/v3.3.2/cluster-configuration.yaml


// 检查日志
kubectl logs -n kubesphere-system $(kubectl get pod -n kubesphere-system -l 'app in (ks-install, ks-installer)' -o jsonpath='{.items[0].metadata.name}') -f


// 查看
kubectl get svc/ks-console -n kubesphere-system

// 启动
minikube service ks-console -n kubesphere-system



---
kubectl apply -f https://github.com/kubesphere/ks-installer/releases/download/v3.2.1/kubesphere-installer.yaml
kubectl apply -f https://github.com/kubesphere/ks-installer/releases/download/v3.2.1/cluster-configuration.yaml

