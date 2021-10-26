# ArgoCD installation
ArgoCD setup. Should be used for all changes regarding ArgoCD setup in [argocd-vs-fluxcd-infrastructure](../../README.md) infrastructure.


## Install
#### Add repo and update cache
```shell
helm repo add argo https://argoproj.github.io/argo-helm
helm repo update
```
#### Override values

```shell
vim values-override.yml
```
or
```shell
nano values-override.yml
```
#### Install chart
```shell
helm -f values-override.yml -n argocd upgrade --install --create-namespace argocd argo/argo-cd
```

#### Add image updater (optional)
Check [image-updater](https://argocd-image-updater.readthedocs.io/en/stable/install/start/) installation guide.

## Make changes
- Pull repo
- Change `values-override.yml` file
- Reinstall helm chart
- Commit and push chages