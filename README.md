Make sure Kubernetes are running in your local machine you can use colima or docker desktop 


# Install Argo CD Helm repository
``` bash
helm repo add argo https://argoproj.github.io/argo-helm
helm repo update
helm upgrade --install argocd argo/argo-cd --namespace argocd --create-namespace
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```
copy the generate password 

## Open separate terminal 
``` bash
kubectl port-forward service/argocd-server -n argocd 8080:443
```
Open localhost:8080 in browser, which shows ArgoCD login page 
Enter user as 'admin' and password as above 


# Configure GitOps Infra via ArgoCD
``` bash
git clone https://github.com/block-deploy-org/veracode-gitops-deployment.git
cd veracode-gitops-deployment/applications
kubctl apply -f vulna.yaml
```
Above Install Helm vulnerable-react-helm-app with below value.yaml @main branch as GitOps

https://github.com/block-deploy-org/veracode-gitops-deployment/blob/main/values/vulna-values.yaml


Dependent Repo 
Helm Chart: https://github.com/block-deploy-org/vulnerable-react-helm-app
Two Container : https://github.com/block-deploy-org/vulnerable-react-app


New Feature Test-1
