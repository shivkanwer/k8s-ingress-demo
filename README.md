# Kubernetes Ingress Demo

```bash
# Deploy the applications

kubectl apply -f application1-deploy-svc.yaml
kubectl apply -f application2-deploy-svc.yaml

# Add the Helm chart for Nginx Ingress
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update

# Install nginx ingress controller
helm install app-ingress ingress-nginx/ingress-nginx \
    --namespace ingress \
    --create-namespace \
    --set controller.replicaCount=2 \
    --set controller.nodeSelector."kubernetes\.io/os"=linux \
    --set defaultBackend.nodeSelector."kubernetes\.io/os"=linux

# Get Ingress Controller public IP address
kubectl get service -n ingress

# Update the service type to ClusterIP instead of LoadBalancer
kubectl apply -f application1-cluster-svc.yaml
kubectl apply -f application2-cluster-svc.yaml
```
