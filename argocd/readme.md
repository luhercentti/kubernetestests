
kubectl port-forward svc/argocd-server -n argocd 8866:443


to view flask-app locally on minikube:
minikube service flask-app-service --url
