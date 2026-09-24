# ingress-nginx

    helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
    helm install ingress-nginx ingress-nginx/ingress-nginx \
      -n ingress-nginx --create-namespace -f values.yaml
