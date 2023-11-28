helm install my-redis \
--namespace redis-dev --create-namespace \
--set password=redisPassword \
--set cluster.externalAccess.enabled=true \
oci://registry-1.docker.io/bitnamicharts/redis-cluster


helm install my-redis \
--namespace redis-dev --create-namespace \
--set password=redisPassword \
oci://registry-1.docker.io/bitnamicharts/redis-cluster


// 删除
helm delete my-redis -n redis-dev

To get your password run:
export REDIS_PASSWORD=$(kubectl get secret --namespace "redis-dev" my-redis-redis-cluster -o jsonpath="{.data.redis-password}" | base64 -d)

You have deployed a Redis&reg; Cluster accessible only from within you Kubernetes Cluster.INFO: The Job to create the cluster will be created.To connect to your Redis&reg; cluster:

1. Run a Redis&reg; pod that you can use as a client:
   kubectl run --namespace redis-dev my-redis-redis-cluster-client --rm --tty -i --restart='Never' \
   --env REDIS_PASSWORD=$REDIS_PASSWORD \
   --image docker.io/bitnami/redis-cluster:7.0.12-debian-11-r2 -- bash

2. Connect using the Redis&reg; CLI:

redis-cli -c -h my-redis-redis-cluster -a $REDIS_PASSWORD


kubectl port-forward service/my-redis-redis-cluster tcp-redis -n redis-dev



helm upgrade redis-cluster ot-helm/redis-cluster --set redisCluster.clusterSize=3 --install --namespace ot-operators



kubectl port-forward service/redis-cluster-leader-headless -n ot-operators 6379:6379




helm install my-release \
--set auth.password=secretpassword \
--set sentinel.enabled=true \
--namespace redis-dev --create-namespace \
oci://registry-1.docker.io/bitnamicharts/redis



helm install --namespace redis-dev my-redis --set auth.password=secretpassword --namespace redis-dev --create-namespace --set "cluster.externalAccess.enabled=true,cluster.externalAccess.service.type=LoadBalancer,cluster.externalAccess.service.loadBalancerIP[0]=load-balancerip-0,cluster.externalAccess.service.loadBalancerIP[1]=load-balancerip-1,cluster.externalAccess.service.loadBalancerIP[2]=load-balancerip-2,cluster.externalAccess.service.loadBalancerIP[3]=load-balancerip-3,cluster.externalAccess.service.loadBalancerIP[4]=load-balancerip-4,cluster.externalAccess.service.loadBalancerIP[5]=load-balancerip-5" oci://registry-1.docker.io/bitnamicharts/redis-cluster




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
