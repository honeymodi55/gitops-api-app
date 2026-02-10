# gitops-api-app
This is a Repository for kubernetes manifests for api-app-end-to-end application 

##### For ArgoCD full installation, you will have to perform some manual steps by going inside the EKS cluster. ####

1. Create the Namespace
<kubectl create namespace argocd>

2. Apply the ArgoCD Manifests
<kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml>

3. Access the ArgoCD API Server
By default, the ArgoCD API server is not exposed with an external IP. You have two main ways to access it:

    Option A: Port Forwarding (Quickest for testing)
    This maps a port on your local machine to the cluster.
<kubectl port-forward svc/argocd-server -n argocd 8080:443>
    You can now access the UI at https://localhost:8080 .

    Option B: Load Balancer (For persistent access)
    If you want a dedicated AWS Load Balancer (ALB/NLB), change the service type:
<kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'>

4. Retrieve the Admin Password
ArgoCD creates a default admin password during installation. It is stored in a Kubernetes secret.




* NOTE: If you delete EKS cluster, ArgoCD will be deleted too. You need to perform the above manual steps again 