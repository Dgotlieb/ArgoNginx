## Instructions

#### ArgoCD server setup
1. Fork this repo
2. Start minikube (e.g. `minikube start`)
3. Create a namespace for ArgoCD:
`kubectl create ns argocd`
4. Install ArgoCD CRD:
`kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml`
5. Enable external traffic to ArgoCD service:
`kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'`
6. Port-forward traffic from port 9090 to ArgoCD service:
`kubectl port-forward svc/argocd-server -n argocd 9090:443`
7. Get your admin password:
`kubectl get secrets/argocd-initial-admin-secret -n argocd  --template={{.data.password}} | base64 -d`
8. On your browser, visit [http://127.0.0.1:9090](http://127.0.0.1:9090)
9. Use username: `admin` and the password obtained in section 7

Full instructions can be found at the ArgoCD [Getting Started guide](https://argo-cd.readthedocs.io/en/stable/getting_started/)

#### Add you repository to ArgoCD
1. Press the `New App button`
<img width="109" alt="image" src="https://github.com/user-attachments/assets/90c433f9-aad1-4a62-bf6c-9ae796c0e3f1">

2. Give it a name (under Application Name)
3. `default` can be used for`Project name`
4. Provide your Github repo URL under `Source` --> `repository URL`, 
<img width="189" alt="image" src="https://github.com/user-attachments/assets/cd4a8555-e76f-4aa2-8756-86908717aa0f">

5. Pick the default option under `Destination` --> `Cluster URL`
<img width="284" alt="image" src="https://github.com/user-attachments/assets/25390c90-f86a-4e3f-894e-2596d6dfe66f">

6. Press on the box showing your app and press `Sync`
