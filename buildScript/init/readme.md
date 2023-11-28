brew install helm
brew install kind

[//]: # (helm repo add mysql-operator https://mysql.github.io/mysql-operator/)

[//]: # (helm repo update)

helm repo add hashicorp https://helm.releases.hashicorp.com
helm search repo hashicorp/consul



kind create cluster --config kind-starter-config.yaml


kubectl apply -f metrics-server.yaml  



kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml
kubectl proxy
kubectl apply -f admin-user.yaml
kubectl -n kubernetes-dashboard create token admin-user | pbcopy



kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml



[//]: # (helm install consul hashicorp/consul --set global.name=consul --create-namespace --namespace consul --values consul-values.yaml)




[//]: # (helm install mysql-operator mysql-operator/mysql-operator --namespace mysql-dev --create-namespace)

[//]: # ()
[//]: # (helm install mycluster mysql-operator/mysql-innodbcluster \)

[//]: # (--namespace mysql-dev \)

[//]: # (--version 2.1.0 \)

[//]: # (--set credentials.root.user='root' \)

[//]: # (--set credentials.root.password='123456' \)

[//]: # (--set credentials.root.host='%' \)

[//]: # (--set serverInstances=3 \)

[//]: # (--set routerInstances=1 \)

[//]: # (--set tls.useSelfSigned=true)

[//]: # ()
[//]: # (nginx 不支持tcp端口转发)

[//]: # (kubectl run --rm -it myshell --image=container-registry.oracle.com/mysql/community-operator -- mysqlsh)

[//]: # ()
[//]: # (kubectl port-forward service/mycluster mysql -n mysql-dev)





[//]: # (helm install my-redis-cluster \)

[//]: # (--namespace redis-cluster --create-namespace \)

[//]: # (--set password=redisPassword \)

[//]: # (--set cluster.externalAccess.enabled=true \)

[//]: # (--set cluster.externalAccess.service.type=NodePort \)

[//]: # (oci://registry-1.docker.io/bitnamicharts/redis-cluster)

[//]: # ()
[//]: # ()
[//]: # (kubectl port-forward service/my-redis-redis-cluster tcp-redis -n redis-dev)

[//]: # ()
[//]: # ()
[//]: # (kubectl port-forward service/consul-server --namespace consul 8500:8500)

[//]: # ()
[//]: # ()
[//]: # (kubectl port-forward service/my-redis-redis-cluster --namespace redis-dev 6379:6379)

[//]: # ()
[//]: # ()
[//]: # (kubectl port-forward service/my-redis-redis-cluster-headless --namespace redis-dev 6379:6379)


[//]: # (helm install my-release \)

[//]: # (--set auth.password=secretpassword \)

[//]: # (--set sentinel.enabled=true \)

[//]: # (--namespace redis-dev --create-namespace \)

[//]: # (oci://registry-1.docker.io/bitnamicharts/redis)

[//]: # ()
[//]: # ()
[//]: # (Redis&reg; can be accessed via port 6379 on the following DNS name from within your cluster:)

[//]: # ()
[//]: # (    my-release-redis.redis-dev.svc.cluster.local for read only operations)

[//]: # ()
[//]: # (For read/write operations, first access the Redis&reg; Sentinel cluster, which is available in port 26379 using the same domain name above.)

[//]: # ()
[//]: # ()
[//]: # ()
[//]: # (To get your password run:)

[//]: # ()
[//]: # (    export REDIS_PASSWORD=$&#40;kubectl get secret --namespace redis-dev my-release-redis -o jsonpath="{.data.redis-password}" | base64 -d&#41;)

[//]: # ()
[//]: # (To connect to your Redis&reg; server:)

[//]: # ()
[//]: # (1. Run a Redis&reg; pod that you can use as a client:)

[//]: # ()
[//]: # (   kubectl run --namespace redis-dev redis-client --restart='Never'  --env REDIS_PASSWORD=$REDIS_PASSWORD  --image docker.io/bitnami/redis:7.0.12-debian-11-r2 --command -- sleep infinity)

[//]: # ()
[//]: # (   Use the following command to attach to the pod:)

[//]: # ()
[//]: # (   kubectl exec --tty -i redis-client \)

[//]: # (   --namespace redis-dev -- bash)

[//]: # ()
[//]: # (2. Connect using the Redis&reg; CLI:)

[//]: # (   REDISCLI_AUTH="$REDIS_PASSWORD" redis-cli -h my-release-redis -p 6379 # Read only operations)

[//]: # (   REDISCLI_AUTH="$REDIS_PASSWORD" redis-cli -h my-release-redis -p 26379 # Sentinel access)

[//]: # ()
[//]: # (To connect to your database from outside the cluster execute the following commands:)

[//]: # ()
[//]: # (    kubectl port-forward --namespace redis-dev svc/my-release-redis 6379:6379 &)

[//]: # (    REDISCLI_AUTH="$REDIS_PASSWORD" redis-cli -h 127.0.0.1 -p 6379)




[//]: # (kubectl port-forward --namespace redis-dev svc/my-release-redis tcp-redis)

[//]: # (kubectl port-forward service/mycluster mysql -n mysql-dev)

[//]: # (kubectl port-forward svc/consul-server http -n consul )

docker image prune
docker system prune


kind load docker-image san-francisco-web:1.0.0


// 数据库
consul

[//]: # (helm install my-release \)

[//]: # (--namespace consul --create-namespace \)

[//]: # (--set domain=consul-domain,gossipKey=secretkey \)

[//]: # (oci://registry-1.docker.io/bitnamicharts/consul)

** Please be patient while the chart is being deployed **

Consul can be accessed within the cluster on port 8300 at my-release-consul-headless.consul-dev.svc.cluster.local

In order to access to the Consul Web UI:

1. Get the Consul URL by running these commands:

   kubectl port-forward --namespace consul-dev svc/my-release-consul-ui 80:80
   echo "Consul URL: http://127.0.0.1:80"

2. Access ASP.NET Core using the obtained URL.

Please take into account that you need to wait until a cluster leader is elected before using the Consul Web UI.

In order to check the status of the cluster you can run the following command:

    kubectl exec -it my-release-consul-0 -- consul members

Furthermore, to know which Consul node is the cluster leader run this other command:

    kubectl exec -it my-release-consul-0 -- consul operator raft list-peers


// redis
helm install my-release \
--set auth.password=secretpassword \
--set sentinel.enabled=true \
--namespace redis-dev --create-namespace \
oci://registry-1.docker.io/bitnamicharts/redis

Redis&reg; can be accessed via port 6379 on the following DNS name from within your cluster:

    my-release-redis.redis-dev.svc.cluster.local for read only operations

For read/write operations, first access the Redis&reg; Sentinel cluster, which is available in port 26379 using the same domain name above.



To get your password run:

    export REDIS_PASSWORD=$(kubectl get secret --namespace redis-dev my-release-redis -o jsonpath="{.data.redis-password}" | base64 -d)

To connect to your Redis&reg; server:

1. Run a Redis&reg; pod that you can use as a client:

   kubectl run --namespace redis-dev redis-client --restart='Never'  --env REDIS_PASSWORD=$REDIS_PASSWORD  --image docker.io/bitnami/redis:7.0.12-debian-11-r2 --command -- sleep infinity

   Use the following command to attach to the pod:

   kubectl exec --tty -i redis-client \
   --namespace redis-dev -- bash

2. Connect using the Redis&reg; CLI:
   REDISCLI_AUTH="$REDIS_PASSWORD" redis-cli -h my-release-redis -p 6379 # Read only operations
   REDISCLI_AUTH="$REDIS_PASSWORD" redis-cli -h my-release-redis -p 26379 # Sentinel access

To connect to your database from outside the cluster execute the following commands:

    kubectl port-forward --namespace redis-dev svc/my-release-redis 6379:6379 &
    REDISCLI_AUTH="$REDIS_PASSWORD" redis-cli -h 127.0.0.1 -p 6379

---

helm install my-release \
--set auth.rootPassword=secretpassword,auth.database=app_database,architecture=replication \
--namespace mysql-cluster --create-namespace \
oci://registry-1.docker.io/bitnamicharts/mysql

Tip:

Watch the deployment status using the command: kubectl get pods -w --namespace mysql

Services:

echo Primary: my-release-mysql.mysql.svc.cluster.local:3306

Execute the following to get the administrator credentials:

echo Username: root
MYSQL_ROOT_PASSWORD=$(kubectl get secret --namespace mysql my-release-mysql -o jsonpath="{.data.mysql-root-password}" | base64 -d)

To connect to your database:

1. Run a pod that you can use as a client:

   kubectl run my-release-mysql-client --rm --tty -i --restart='Never' --image  docker.io/bitnami/mysql:8.0.34-debian-11-r8 --namespace mysql --env MYSQL_ROOT_PASSWORD=$MYSQL_ROOT_PASSWORD --command -- bash

2. To connect to primary service (read/write):

   mysql -h my-release-mysql.mysql.svc.cluster.local -uroot -p"$MYSQL_ROOT_PASSWORD"


Tip:

Watch the deployment status using the command: kubectl get pods -w --namespace mysql-cluster

Services:

echo Primary: my-release-mysql-primary.mysql-cluster.svc.cluster.local:3306
echo Secondary: my-release-mysql-secondary.mysql-cluster.svc.cluster.local:3306

Execute the following to get the administrator credentials:

echo Username: root
MYSQL_ROOT_PASSWORD=$(kubectl get secret --namespace mysql-cluster my-release-mysql -o jsonpath="{.data.mysql-root-password}" | base64 -d)

To connect to your database:

1. Run a pod that you can use as a client:

   kubectl run my-release-mysql-client --rm --tty -i --restart='Never' --image  docker.io/bitnami/mysql:8.0.34-debian-11-r8 --namespace mysql-cluster --env MYSQL_ROOT_PASSWORD=$MYSQL_ROOT_PASSWORD --command -- bash

2. To connect to primary service (read/write):

   mysql -h my-release-mysql-primary.mysql-cluster.svc.cluster.local -uroot -p"$MYSQL_ROOT_PASSWORD"

3. To connect to secondary service (read-only):

   mysql -h my-release-mysql-secondary.mysql-cluster.svc.cluster.local -uroot -p"$MYSQL_ROOT_PASSWORD"

---
create schema `san-francisco` collate utf8mb4_general_ci;
mysql -h127.0.0.1 -P3306 -uroot -p
jdbc:mysql://127.0.0.1:3306/san-francisco?characterEncoding=UTF-8&failOverReadOnly=false&secondsBeforeRetryMaster=0&queriesBeforeRetryMaster=0&serverTimezone=Asia/Shanghai&useUnicode=true&&allowPublicKeyRetrieval=true&useSSL=false&connectTimeout=10000&socketTimeout=60000


kubectl port-forward svc/my-release-redis tcp-redis --namespace redis-dev
kubectl port-forward svc/consul-client http -n consul-dev
kubectl port-forward svc/my-release-mysql-primary-headless mysql -n mysql-cluster