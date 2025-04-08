minikube start --memory=8192mb --cpus=4


kubectl apply -f app-test-istio.yaml


#to view ips with porst to access your app through istio redirection
minikube service istio-ingressgateway -n istio-system


to check ingress config: #COMMAND1
kubectl get svc -n istio-system istio-ingressgateway 
NAME                   TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)                                      AGE
istio-ingressgateway   LoadBalancer   10.99.147.127   <pending>     15021:30267/TCP,80:31838/TCP,443:31969/TCP   7d19h

The <pending> status appears because you're using the LoadBalancer service type for the Istio ingress gateway. In a cloud environment (AWS, GCP, Azure), this would trigger the provisioning of an actual load balancer with an external IP. However, Minikube runs locally and doesn't have the capability to provision real cloud load balancers.


The process works like this:

Your istio-ingressgateway service is of type LoadBalancer
Since there's no actual cloud load balancer, Kubernetes still assigns a NodePort to the service (31838 for port 80)
Minikube then creates a port forward from your localhost to that NodePort (PORTGIVENBYCOMMAND #COMMAND1 → 31838)
This allows you to access the service without needing to run minikube tunnel

Since you were able to access the nginx page through port PORTGIVENBYCOMMAND #COMMAND1 (which is mapped to port 80 of the ingress gateway), this confirms that:

Your Istio ingress gateway is working correctly
The VirtualService is properly routing traffic to your nginx service
The nginx pod is serving content as expected
All the Istio components (sidecar proxy, etc.) are functioning