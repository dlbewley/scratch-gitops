# Given this setup

Argo-apps/ holds Applications which may (probably do) point off to remote git repositories.

```
 .
├──  argo-apps
│  ├──  cfg
│  │  ├──  metallb
│  │  │  ├──  application.yaml
│  │  │  └──  kustomization.yaml
│  │  ├──  nmstate
│  │  ├──  readme.md
│  │  └──  rhacm
│  ├──  olm
│  │  ├──  kustomization.yaml
│  │  ├──  metallb
│  │  │  ├──  application.yaml
│  │  │  └──  kustomization.yaml
│  │  ├──  nmstate
│  │  │  ├──  application.yaml
│  │  │  └──  kustomization.yaml
│  │  ├──  readme.md
│  │  └──  rhacm
│  │     ├──  application.yaml
│  │     └──  kustomization.yaml
│  └──  readme.md
├──  cluster
│  ├──  hub
│  │  ├──  application.yaml
│  │  ├──  kustomization.yaml
│  │  └──  readme.md
│  └──  readme.md
└──  readme.md
```

# Create [the argo](cluster/hub/application.yaml) app to manage the Hub cluster 

This will also create the other apps referenced via the [kustomization](cluster/hub/kustomization.yaml). Should they be abstracted further? What's an app of apps?

```bash
$ oc apply -k cluster/hub
application.argoproj.io/cluster-hub-config configured
application.argoproj.io/metallb-operator configured
application.argoproj.io/metallb-config configured
application.argoproj.io/nmstate-operator configured
application.argoproj.io/rhacm-operator configured
```

# Manually sync the apps in the ArgoCD UI and then:

```bash
$ oc get application.argoproj.io -A
NAMESPACE          NAME                 SYNC STATUS   HEALTH STATUS
openshift-gitops   cluster-hub-config   Synced        Healthy
openshift-gitops   metallb-config       Synced        Healthy
openshift-gitops   metallb-operator     Synced        Healthy
openshift-gitops   nmstate-operator     Synced        Healthy
openshift-gitops   rhacm-operator       Synced        Healthy
```

