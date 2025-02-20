The config for the cluster known as 'hub'.

Need to add rbac here for everything argo needs to patch. eg.

> error when patching "/dev/shm/3268188094": nmstates.nmstate.io "nmstate" is forbidden: User "system:serviceaccount:openshift-gitops:openshift-gitops-argocd-application-controller" cannot patch resource "nmstates" in API group "nmstate.io" at the cluster scope

> nodenetworkconfigurationpolicies.nmstate.io is forbidden: User "system:serviceaccount:openshift-gitops:openshift-gitops-argocd-application-controller" cannot create resource "nodenetworkconfigurationpolicies" in API group "nmstate.io" at the cluster scope

> nodenetworkconfigurationpolicies.nmstate.io is forbidden: User "system:serviceaccount:openshift-gitops:openshift-gitops-argocd-application-controller" cannot create resource "nodenetworkconfigurationpolicies" in API group "nmstate.io" at the cluster scope

