## Prepare database for repository

A MongoDB replica set is used to persistent repository content. You can follow the steps below to install one to the GKE cluster. It is a single node replica set, can only be used to experiment features. Please follow the MongoDB document to install a product-ready replica set for prodcution deployment.

### Setup helm repository

You should have a credentials (username/password) from Precisely for the helm registry,
```
helm repo add spatial https://gitlab.com/api/v4/projects/24255413/packages/helm/stable --username <username> --password <password>
```
```
helm repo update
```
```
helm search repo spatial
```

Create a secret for image pull (using the same credentials)
```
kubectl -n spatial create secret docker-registry regcred-gitlab --docker-server=registry.gitlab.com --docker-username=<username> --docker-password=<password>
```

### Install a MongoDB instance by helm

Install MongoDB pod from helm chart
```
helm install postgis spatial/mongo-standalone --version 1.0.0
```
```
kubectl get pod
```
Wait until the mongo pod is ready
```
NAME                                      READY   STATUS    RESTARTS   AGE
mongo                                     1/1     Running   0          8m35s
```
This will install a single node replica set instance without authentication
```
connection uri = mongodb://mongo:27017/
```

### [Next Step](deploy-spatial-services.md)
