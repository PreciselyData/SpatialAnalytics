## Prepare database for repository

A Database (PostgreSQL or MSSQL Server) instance is used to persistent repository content. If you have an external instance available, just collect the connection string and credentials for further use. You can also follow the steps below to install a postgres database to the GKE cluster. For the performance reason, keep the database instance as close to the cluster as possible.

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

### Install a postgres database instance by helm

Install postgres pod from helm chart
```
helm install postgis spatial/postgis-standalone --version 1.0.0 -n spatial
```
```
kubectl get pod
```
Wait until the postgis pod is ready
```
NAME                                      READY   STATUS    RESTARTS   AGE
postgis                                   1/1     Running   0          8m35s
```
This will install a postgre single node instance with the following information (default)
```
connection uri = jdbc:postgresql://postgis:5432/jackrabbit_db?currentSchema=public
username: "jackrabbit_user"
password: "jackrabbit_user"
```

### [Next Step](deploy-spatial-services.md)
