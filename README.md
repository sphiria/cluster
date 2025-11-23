# sphiria - k8s

### 1password operator

```bash
helm repo add 1password https://1password.github.io/connect-helm-charts
helm install connect 1password/connect --set-file connect.credentials=1password-credentials.json --set operator.create=true --set operator.token.value=OP_CONNECT_TOKEN
```

### cert-manager

```bash
helm repo add jetstack https://charts.jetstack.io
helm repo update
kubectl create namespace cert-manager
helm install cert-manager jetstack/cert-manager \
  --namespace cert-manager \
  --version v1.19.1 \
  --set installCRDs=true
```

### nginx ingress controller

```bash
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
kubectl create namespace ingress-nginx
helm install ingress-nginx ingress-nginx/ingress-nginx --namespace ingress-nginx -f charts/nginx/values.yaml
```

### monitoring

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm install kube-prometheus-stack prometheus-community/kube-prometheus-stack -n monitoring --create-namespace -f charts/kube-prometheus-stack/values.yaml
helm install loki grafana/loki -n monitoring -f charts/loki/values.yaml
kubectl apply -f charts/loki/grafana-datasource.yaml
helm repo add vector https://helm.vector.dev
helm install vector vector/vector -n monitoring -f charts/vector/values.yam
```

### argocd
```bash
helm repo add argo https://argoproj.github.io/argo-helm
helm install argocd argo/argo-cd \
    --namespace argocd \
    --create-namespace \
    -f charts/argocd/values.yaml
```

### mariadb

```bash
kubectl apply -f mariadb
```

### prod
helm upgrade --install gbf-wiki charts/gbf-wiki -n wiki
