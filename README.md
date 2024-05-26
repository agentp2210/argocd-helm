1. Install the chart for guestbook
``` shell
helm install guestbook ./helm-guestbook
```

2. Install argocd
``` shell
helm install argocd oci://ghcr.io/argoproj/argo-helm/argo-cd -n argocd --set server.service.type=LoadBalancer
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