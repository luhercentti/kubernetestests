
minikube start --memory=8192mb --cpus=4 --profile linkerd

minikube profile list
minikube stop -p minikube

minikube start -p linkerd