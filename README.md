# aro-configs

This space is used to demonstate the ArgoCD capabilities to maintain ARO cluster configurations as well as application configurations. In order to demonstrate it successfully, below tasks are required.

# 1. Deployment of ArgoCD Operator in ARO cluster

### Pre-Requisites:
    1. Openshift cluster is up and running
    2. OC CLI is able to access the cluster

### Steps

1. Install `Red Hat OpenShift GitOps` under `Operators` tab
2. Assign permissions 
    ```
    oc adm policy add-cluster-role-to-user cluster-admin system:serviceaccount:openshift-gitops:openshift-gitops-argocd-application-controller -n openshift-gitops
    ```

# 2. Synchronization of cluster configuration

Refer the link [HERE](https://github.com/adi-sharma14/aro-configs/tree/main/argo) for ArgoCD application manifests 

### Pre-Requisites:
    1. Openshift cluster is up and running
    2. Operator `Red Hat OpenShift GitOps` is successfuly installed
    3. ArgoCD UI is up and running
    4. GITHUB_TOKEN is set as env variable for the repo

### Steps

* Deploy the argoCD applications to synch cluster configuration
    ```
    oc apply -f ../cluster/secret.yml
    oc apply -f cluster-configs.yml
    ```

# 3. Deployment of application using S2I

S2I is one of the build strategy to build the images using the source code only. Dockerfiles are not required.

* Refer the link [HERE](https://github.com/adi-sharma14/demo-app.git) for sample web application source code.

* Refer the link [HERE](https://github.com/adi-sharma14/aro-configs/tree/main/s2iapp) - these manifests are used for app deployment on ARO cluster using S2I build strategy.

### Steps

* Deploy the argoCD applications to deploy the webapp using **S2I build strategy**
    ```
    oc apply -f s2iapp-configs.yml
    ```
