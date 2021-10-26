# argocd-vs-fluxcd-infrastructure

## Description

This is a project with infrastructure, based on:
 
- [OTC CCE](https://open-telekom-cloud.com/en/products-services/cloud-container-engine)
- [Argo CD](https://argo-cd.readthedocs.io/en/stable/)
- [Flux](https://fluxcd.io)

[Git repository](https://github.com/iits-consulting/argocd-vs-fluxcd-application) with a dummy application and CI that was used here

## Purposes

**OTC Event:** [A battle of GitOps tools: Argo CD vs Flux](https://community.open-telekom-cloud.com/community?id=community_event&sys_id=8a84320fb7763450d15aa7b16b8c0222)

## Structure of the repository

```
├── argocd    <--    # Argo CD setup
├── chart     <--    # Helm Chart of the Application
└── flux      <--    # Flux setup
```

## Argo CD

```
./argocd/
├── install
├── projects
│   ├── development
│   |   └── argocd-app-dev.yml
│   └── production
│       └── argocd-app-prod.yml
└── stages                           <-- # Application with different (per-stage) parameters
    ├── development
    |   └── argocd-vs-fluxcd.yml
    └── production
        └── argocd-vs-fluxcd.yml

```

## Flux

```
./flux/
├── app
│   ├── base                       <-- # Common Kubernetes objects that describe the application
│   |   └── deployment.yaml
│   ├── production
│   |   └── kustomization.yaml     <-- # Environment-specific changes to the base objects
│   └── staging
│       └── kustomization.yaml
├── clusters                       <-- # Entry point for the Flux Kustomization controllers
│   ├── production
│   |   ├── app.yaml               <-- # Description of the Application using Kustomize
│   |   ├── image-update.yaml      <-- # Automated updates of the image tags
│   |   └── infrastructure.yaml    <-- # Common infrastructure described using Helm Charts
│   └── staging
│       ├── app.yaml
│       ├── image-update.yaml
│       └── infrastructure.yaml
├── image-update
│   ├── production
│   |   ├── automation.yaml        <-- # Opens a new pull request to the main branch
│   |   ├── image-policy.yaml      <-- # Required range of the Docker image versions
│   |   └── image-repository.yaml  <-- # Path to the Docker repository
|   └── staging
│       ├── automation.yaml
│       ├── image-policy.yaml
│       └── image-repository.yaml
├── infrastructure                 <-- # Helm Charts for the third-party dependencies
|   └── redis
|       ├── helm-release.yaml
|       └── helm-repository.yaml
└── install                        <-- # Kubernetes objects that describe Flux. Generated by Flux CLI tool
    ├── flux-system.yaml           <-- # Namespace, CRDs, Deployments, etc that Flux requires
    └── git-repository.yaml        <-- # Access to the git repository (this one) that describes the infrastructure
```
