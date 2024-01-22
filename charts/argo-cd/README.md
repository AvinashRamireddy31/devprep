## Description
Reference link: https://www.arthurkoziel.com/setting-up-argocd-with-helm/

We need to generate a Helm chart lock file first.
When installing a Helm chart, Argo CD checks the lock file for any dependencies and downloads them. Not having the lock file will result in an error
`Error: found in Chart.yaml, but missing in charts/ directory: argo-cd`

## Commands

`helm repo add argo-cd https://argoproj.github.io/argo-helm`
`helm dep update .`

`echo "**/charts/*.tgz" >> .gitignore`

`helm upgrade --install argo-cd .`

`kubectl port-forward svc/argo-cd-argocd-server 8080:443`

We can then visit http://localhost:8080 to access it, which will show as a login form. The default username is `admin`
The password is auto-generated, we can get it with:

`kubectl get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d`
