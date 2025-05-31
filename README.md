
PROJECT : GitOps Workflow with ArgoCD and Kubernetes (Local Setup using Minikube)

Objective:
Implement GitOps by syncing Kubernetes deployment states directly from a Git repository using ArgoCD, running locally via Minikube.

Tools Used:
•	Minikube (Local Kubernetes)
•	ArgoCD (Open Source GitOps Tool)
•	GitHub (Manifest Repository)
•	Docker (For Image Building)
•	VS Code (For YAML Editing)

Step-by-Step Guide:

1.  Prerequisites
•	Install Docker Desktop
•	Install Minikube
•	Install kubectl
•	Install ArgoCD CLI (optional)
•	VS Code installed with YAML support
•	GitHub account

2. Start Minikube
minikube start

3. Install ArgoCD
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml


 4.  Access ArgoCD UI
kubectl port-forward svc/argocd-server -n argocd 8080:443

Visit [https://localhost:8080](https://localhost:8080)

 5.  Login to ArgoCD
kubectl get pods -n argocd
kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | base64 -d

Login with:
	Username: admin
	Password: <above-password>


 6. Create GitHub Repo
Push your Kubernetes YAML manifests (deployment.yaml, service.yaml, etc.) to a public/private GitHub repo.


 7.  Add App to ArgoCD
kubectl apply -f app.yaml


 8. Observe GitOps in Action
i.	ArgoCD will auto-sync and deploy your app.
ii.	Make changes in GitHub, ArgoCD reflects it automatically.

Cleanup:
To pause your cluster:
minikube stop

 To delete the setup completely:
minikube delete


Implemented GitOps pipeline using ArgoCD and Kubernetes with Minikube for automated, declarative application delivery. 
