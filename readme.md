# Given this simple setup

```
.
├── argo-apps
│  └── cluster-hub-configs
├── cluster
│  └── hub
└── readme.md
```

# Create the argo app

```bash
$ oc apply -k argo-apps/cluster-hub-configs
```

<details>
  <summary>Application source</summary>
```yaml
$ oc kustomize argo-apps/cluster-hub-configs
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: cluster-hub-configs
  namespace: openshift-gitops
spec:
  destination:
    namespace: openshift-gitops
    server: https://kubernetes.default.svc
  project: default
  source:
    directory:
      recurse: false
    path: cluster/hub
    repoURL: https://github.com/dlbewley/scratch-gitops.git
    targetRevision: HEAD
  sources: []
```
<details>

Above will create this "application sub resource" (what is the result of an `Application.argoproj.io` called?)

<details>
  <summary>Synced Application source</summary>
```yaml
$ oc kustomize cluster/hub
apiVersion: v1
kind: Namespace
metadata:
  name: demo-virt
```
</details>

Manually sync the app in the ArgoCD UI and then:

```bash
$ oc get applications -A
NAMESPACE          NAME                  SYNC STATUS   HEALTH STATUS
openshift-gitops   cluster-hub-configs   Synced        Healthy

# created by the app:
oc get namespace demo-virt
NAME        STATUS   AGE
demo-virt   Active   4m45s
```

