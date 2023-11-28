minikube start --cpus=3 --memory=12288mb --driver=hyperkit --cni=calico --nodes=2

minikube start --cpus=4 --memory=8G --driver=hyperkit --nodes=3
minikube start --cpus=4 --memory=8G --nodes=3

minikube addons enable metrics-server

minikube addons enable ingress

minikube addons enable dashboard


minikube start --cpus=6 --memory=12288mb

