1. Install nginx ingress-controller
``` shell
helm install nginx-ingress oci://ghcr.io/nginxinc/charts/nginx-ingress
```

1. Install the chart for guestbook
``` shell
helm install guestbook ./helm-guestbook
```

2. Install argocd
``` shell
helm install argocd oci://ghcr.io/argoproj/argo-helm/argo-cd -n argocd --set server.service.type=LoadBalancer --create-namespace
```

3. Create an app in Argo CD
``` shell
helm install argocdapp ./apps
```

4. Get password from the secret
``` shell
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

5. Get ArgoCD URL
``` shell
kubectl get svc argocd-server -n argocd -o jsonpath="{.status.loadBalancer.ingress[0].hostname}"
```

6. Access the URL and sync the app