# Steps I followed to run the argocd UI

1. `kubectl create namespace argocd`
1. `kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml`
1. Get the list of services running on argocd namespace:<br/>`kubectl get svc -n argocd`
1. Expose argocd port 443 to local 8080:<br/>`kubectl port-forward -n argocd svc/argocd-server 8080:443`
1. Get the argocd password which is stored in `argocd` namespace with key named `argocd-initial-admin-secret`:<br/>`kubernetes-argocd % kubectl get secrets argocd-initial-admin-secret -n argocd -o yaml`
<br/>
<br/>
Output of this will be like this:
    ```apiVersion: v1
    data:
        password: sdvsdDVSDVSdvDSFVSAascvads==
    kind: Secret
    metadata:
        creationTimestamp: "2024-05-26T08:59:03Z"
        name: argocd-initial-admin-secret
        namespace: argocd
        resourceVersion: "23624"
        uid: sdvsdvsd-3122-22sa-22sd-b44sds5cac
    type: Opaque```

1. Decode the base64 password and login to argocd in localhost: [localhost:8080]:<br/>
`echo sdvsdDVSDVSdvDSFVSAascvads== | base64 --decode`
1. Add application.yaml with kind `aplication` and fill the metadata, or you can create an application in argocd UI and run a cluster
1. If application.yaml is created manually then apply the changes with:<br/>`kubectl apply -f application.yaml`