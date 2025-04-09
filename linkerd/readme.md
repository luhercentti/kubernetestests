
minikube start --memory=8192mb --cpus=4 --profile linkerd

minikube profile list
minikube stop -p minikube

minikube start -p linkerd



linkerd:


kubectl get -n emojivoto deploy -o yaml \
  | linkerd inject - \
  | kubectl apply -f -




linkerd viz dashboard &

kubectl port-forward -n linkerd-viz svc/web 8084:8084
