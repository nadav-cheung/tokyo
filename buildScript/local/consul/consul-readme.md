brew install helm

helm repo add hashicorp https://helm.releases.hashicorp.com
helm search repo hashicorp/consul
kubectl get namespace
helm install consul hashicorp/consul --set global.name=consul --create-namespace --namespace consul-dev --values values.yaml


kubectl apply -f consul-client.yaml


创建helm生成的文件

helm template consul/ --output-dir ./result

kubectl port-forward service/consul-server --namespace consul 8500:8500

helm delete consul -n consul

minikube service consul-ui -n consul