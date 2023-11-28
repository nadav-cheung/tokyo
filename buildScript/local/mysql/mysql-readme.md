https://dev.mysql.com/doc/mysql-operator/en/mysql-operator-installation-helm.html
https://github.com/mysql/mysql-operator

helm repo add mysql-operator https://mysql.github.io/mysql-operator/
helm repo update

helm show values mysql-operator/mysql-innodbcluster
helm show values mysql-operator/mysql-innodbcluster >> deploy-cluster.yaml

helm show values mysql-operator/mysql-operator >> deploy-crds.yaml

helm template mysql-operator mysql-operator/mysql-operator --namespace mysql-operator --create-namespace --output-dir
./result

helm template mysql-operator mysql-operator/mysql-operator --namespace mysql-operator --create-namespace --values
deploy-crds.yaml --output-dir ./result-crds

helm install mycluster mysql-operator/mysql-innodbcluster
helm template mycluster mysql-operator/mysql-innodbcluster

helm template mycluster mysql-operator/mysql-innodbcluster \
--set credentials.root.user='root' \
--set credentials.root.password='sakila' \
--set credentials.root.host='%' \
--set serverInstances=3 \
--set routerInstances=1 \
--set tls.useSelfSigned=true --output-dir ./result-cluster

helm template mycluster mysql-operator/mysql-innodbcluster \
--set credentials.root.user='root' \
--set credentials.root.password='sakila' \
--set credentials.root.host='%' \
--set serverInstances=3 \
--set routerInstances=1 \
--set tls.useSelfSigned=true \
--namespace mycluster >> mycluster.cluster.yaml

helm install mysql-operator mysql-operator/mysql-operator --namespace mysql-dev --create-namespace
helm install mycluster mysql-operator/mysql-innodbcluster \
--namespace mysql-operator \
--create-namespace \
--set credentials.root.user='root' \
--set credentials.root.password='123456' \
--set credentials.root.host='%' \
--set serverInstances=3 \
--set routerInstances=1 \
--set tls.useSelfSigned=true

helm install mysql-operator mysql-operator/mysql-operator --namespace mysql-operator --create-namespace
helm install mycluster mysql-operator/mysql-innodbcluster --namespace mysql-dev --create-namespace \
--set credentials.root.user='root' \
--set credentials.root.password='123456' \
--set credentials.root.host='%' \
--set serverInstances=3 \
--set routerInstances=1 \
--set tls.useSelfSigned=true

helm template mysql-operator mysql-operator/mysql-operator --namespace mysql-operator --create-namespace >>
mysql-operator.yaml
helm template mycluster mysql-operator/mysql-innodbcluster --namespace mysql-operator \
--set credentials.root.user='root' \
--set credentials.root.password='123456' \
--set credentials.root.host='%' \
--set serverInstances=3 \
--set routerInstances=1 \
--set tls.useSelfSigned=true >> mycluster.yaml

// 查看主节点
select * from performance_schema.replication_group_members;

helm install mysql-operator mysql-operator/mysql-operator --namespace mysql-operator --create-namespace
helm upgrade mycluster mysql-operator/mysql-innodbcluster --namespace mysql-dev --create-namespace \
--set credentials.root.user='root' \
--set credentials.root.password='123456' \
--set credentials.root.host='%' \
--set serverInstances=2 \
--set routerInstances=1 \
--set tls.useSelfSigned=true

// 端口
kubectl port-forward service/mycluster mysql -n mysql-dev

helm install mycluster mysql-operator/mysql-innodbcluster --namespace mysql-dev --create-namespace \
--set credentials.root.user='root' \
--set credentials.root.password='123456' \
--set credentials.root.host='%' \
--set serverInstances=2 \
--set routerInstances=1 \
--set tls.useSelfSigned=true

helm install mysql-operator mysql-operator/mysql-operator --namespace mysql-dev --create-namespace

helm install mycluster mysql-operator/mysql-innodbcluster \
--namespace mysql-dev \
--set credentials.root.user='root' \
--set credentials.root.password='123456' \
--set credentials.root.host='%' \
--set serverInstances=3 \
--set routerInstances=1 \
--set tls.useSelfSigned=true

nginx 不支持tcp端口转发

kubectl run --rm -it myshell --image=container-registry.oracle.com/mysql/community-operator -- mysqlsh

kubectl port-forward service/mycluster mysql -n mysql-dev
