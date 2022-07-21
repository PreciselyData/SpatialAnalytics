## Deploy spatial services using helm charts

### Setup helm repository

You should have a credentials from Precisely for the helm registry,
```
helm repo add spatial https://gitlab.com/api/v4/projects/24255413/packages/helm/stable --username <username> --password <password>
```
```
helm repo update
```
```
helm search repo spatial --devel
```

Create a secret for image pull (using the same credentials)
```
kubectl -n spatial create secret docker-registry regcred-gitlab --docker-server=registry.gitlab.com --docker-username=<username> --docker-password=<password>
```


### Deploy Spatial Services

There are two deployment files to choose from that requires different resources (CPU and Memory). Start from the small one (`gitlab-deployment-small-values.yaml`). If you use your external Postgres Database, update the information in the manifest file `values-jackrabbit-postgres.yaml`. The value of the `global.ingress.host` is the Ingress External IP.
```
helm install spatial spatial/spatial-cloud-native --version 1.0.0-SNAPSHOT -n spatial -f gitlab-deployment-small-values.yaml -f values-jackrabbit-postgres.yaml --set global.ingress.host=<your external ip>
```

After all the pods in namespace 'spatial' are in 'ready' status, launch SpatialServerManager in a browser with the URL below. By default, the security is off, so you can login with any username/password. You should be able to browser named resources and pre-view maps.
https://<your external ip>/SpatialServerManager
    
The last step of the deployment is to make the final configuation (you can do it later). See [Configuring Your System](https://docs.precisely.com/docs/sftw/spectrum/22.1/en/webhelp/Spatial/Spatial/source/Administration/load_balancing/configurespectrum_introduction.html)
