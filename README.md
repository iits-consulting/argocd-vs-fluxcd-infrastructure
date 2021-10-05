# argocd-vs-fluxcd-infrastructure
### Description
This is a project with infrastructure, based on:
 - [Terraform](https://www.terraform.io)
 - [OTC CCE](https://open-telekom-cloud.com/en/products-services/cloud-container-engine)
 - [ArgoCD](https://argo-cd.readthedocs.io/en/stable/)
 - [FluxCD](https://fluxcd.io)

[Repo](https://github.com/iits-consulting/argocd-vs-fluxcd-application) with dummy application and CI that was used here
### Purposes
**OTC Event:** [_A battle of GitOps tools: Argo CD vs Flux CD_](https://community.open-telekom-cloud.com/community?id=community_event&sys_id=8a84320fb7763450d15aa7b16b8c0222)

### Repo structure
```
argocd-vs-fluxcd-infrastructure
│
│   LICENSE
│   README.md
│
└───k8s-cluster
│   │
│   └─── terraform    -------------->    # Everything to prepare Environment
│   │     ─  main.tf
│   │     ─  variables.tf
│   │     ─  versions.tf
│   │
│   └─── fluxcd    ----------------->    # FluxCD setup
│   │     ─  flux-cd helmchart
│   │
│   └─── argocd     ---------------->    # ArgoCD setup
│         ─  argo-cd helmchart
│
│   
└───fluxcd    ---------------------->    # Applications described by Flux

│   └─── stages    ----------------->    # Application with different (per-stage) parameters
│       │
│       └───development
│       │     ─  my-application.yml
│       │
│       └───production
│             ─  my-application.yml
│
│
└───argocd    ---------------------->    # Applications described by Argo
    │
    └─── stages    ----------------->    # Application with different (per-stage) parameters
        │
        └───development
        │     ─  my-application.yml
        │
        └───production
              ─  my-application.yml
```
