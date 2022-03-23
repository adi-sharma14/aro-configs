# aro-configs

This space is used to demonstate the ArgoCD capabilities to maintain ARO cluster configurations. In order to demonstrate it successfully, below tasks are required.

# 1. Deployment of ArgoCD Operator in ARO cluster

### Pre-Requisites:
    1. Openshift cluster is up and running

### Steps

1. Install `Red Hat OpenShift GitOps` under `Operators` tab
2. Assign permissions 
    ```
    oc adm policy add-cluster-role-to-user cluster-admin system:serviceaccount:openshift-gitops:openshift-gitops-argocd-application-controller -n openshift-gitops
    ```

# 2. Synchronization of cluster configuration, self-heal and prune

Refer the link here for ArgoCD application manifests [code](https://github.com/adi-sharma14/aro-configs/argo)

### Pre-Requisites:
    1. Openshift cluster is up and running
    2. Operator `Red Hat OpenShift GitOps` is successfuly installed
    3. ArgoCD UI is up and running

### Steps

* Deploy the argoCD applications to synch cluster configuration
    ```
    oc apply -f cluster-configs.yml
    oc apply -f s2iapp-configs.yml
    oc apply -f springapp-configs.yml
    ```

# 3. Deployment of application using S2I

Refer the link here for ArgoCD application manifests [code](https://github.com/adi-sharma14/aro-configs/s2iapp)

### Pre-Requisites:
    1. Openshift cluster is up and running
    2. Operator `Red Hat OpenShift GitOps` is successfuly installed
    3. ArgoCD UI is up and running
    4. `cluster-configs` app is healthy in argoCD

### Steps

* Deploy the argoCD applications to showcase S2I capability
    ```
    oc apply -f s2iapp-configs.yml
    ```

# 4. Deployment of application using Docker strategy

Refer the link here for ArgoCD application manifests [code](https://github.com/adi-sharma14/aro-configs/app)

### Pre-Requisites:
    1. Openshift cluster is up and running
    2. Operator `Red Hat OpenShift GitOps` is successfuly installed
    3. ArgoCD UI is up and running
    4. `cluster-configs` app is healthy in argoCD

### Steps

* Deploy the argoCD applications to synch cluster configuration
    ```
    oc apply -f springapp-configs.yml
    ```