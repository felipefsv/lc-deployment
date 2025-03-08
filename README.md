# lc-deployment
Manifesto Kubernetes projeto LC


# Instalação Longhorn

kubectl apply -f https://raw.githubusercontent.com/longhorn/longhorn/master/deploy/longhorn.yaml

- Expor painel Longhorn: 
    - kubectl -n longhorn-system expose deployment longhorn-ui --type=NodePort --overrides='{"spec": {"ports": [{"nodePort": 30080, "port": 8000, "target": 8000}]}}' --port=8000


# Instalação e configuração ArgoCD

- kubectl create namespace argocd

- kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/v2.14.2/manifests/install.yaml

- Expor servico argocd-server
    - kubectl patch svc argocd-server -p '{"spec": {"type": "NodePort"}}' -n argocd

- Senha inicial ADMIN
    - kubectl get secrets argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | base64 --decode