Implementar argo

k create namespace argocd
k apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

Aplicar ingress

Expor argo:
k patch svc argocd-server -n argocd -p '{"spec": {"type": "NodePort"}}'

Recuperar senha que é gerada automaticamente:
k -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

Criar aplicação no argo e pronto

Teste de sync:
k scale deployment devops-front-dev --replicas=2