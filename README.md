# Implementar argo

Passos:
1. Criar namespaces  
1.1 `kubectl create namespace argocd`  
1.2 `kubectl create namespace argo-rollouts`
2. Aplicar manifestos argo  
2.1 `kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml`  
2.2 `kubectl apply -n argo-rollouts -f https://github.com/argoproj/argo-rollouts/releases/latest/download/install.yaml`  
2.3 `kubectl apply -n argo-rollouts -f https://github.com/argoproj/argo-rollouts/releases/latest/download/dashboard-install.yaml`  

3. Aplicar ingress do argo  
`kubectl apply -f ingress.yaml`

4. Expor argo:  
`kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "NodePort"}}'`

5. Recuperar senha do argo que é gerada automaticamente:  
`kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d`  
* Senha padrão: admin
* acesso na porta 32520
* acesso na porta 3100

6. Aplicar ingress nginx controller:  
`kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.14.0/deploy/static/provider/cloud/deploy.yaml`

7. Aplicar manifestos do Cloud native pg:  
`kubectl apply --server-side -f \
  https://raw.githubusercontent.com/cloudnative-pg/cloudnative-pg/release-1.27/releases/cnpg-1.27.1.yaml`

Criar as aplicações no argo aplicando os manifestos desse respositório.