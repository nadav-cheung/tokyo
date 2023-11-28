kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml

kubectl proxy


kubectl apply -f admin-user.yaml   


kubectl -n kubernetes-dashboard create token admin-user