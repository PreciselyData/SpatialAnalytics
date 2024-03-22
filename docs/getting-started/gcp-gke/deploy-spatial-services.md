## Deploy spatial services using helm charts

### Deploy Spatial Services

Create a secret for image pull (using given credentials)
```
kubectl -n spatial create secret docker-registry regcred-gitlab --docker-server=registry.gitlab.com --docker-username=<username> --docker-password=<password>
```


There are two deployment files to choose from that require different amount of resources (CPU and Memory). Start from the small one (`~/SpatialAnalytics/deploy/gitlab-deployment-small-values.yaml`). A production deployment should use `~/SpatialAnalytics/deploy/gitlab-deployment-values.yaml`.

Note: if you are not using MongoDB deployed from this guide, you need to update the mongo uri before install.

```
helm install spatial ~/SpatialAnalytics/charts/spatial-cloud-native-1.1.0.tgz -f ~/SpatialAnalytics/deploy/gitlab-deployment-small-values.yaml
```
Wait until all services are ready. It may take 5 to 8 minutes to get ready for the first time. 
```
kubectl get pod
```

You can also deploy services with hpa enabled, here is an example (check [gitlab-deployment-values.yaml](../../../deploy/gitlab-deployment-values.yaml) for more details),
```
helm install spatial ~/SpatialAnalytics/charts/spatial-cloud-native-1.1.0.tgz -f ~/SpatialAnalytics/deploy/gitlab-deployment-values.yaml --set mapping-service.hpaEnabled=true --set mapping-service.maxReplicaCount=3
```

After all the pods are in 'ready' status, launch SpatialServerManager in a browser with the URL below (You may need to accept the default self-signed certificate from Ingress. Check out the ingress document on how to change the certificate if you need). By default, the security is off, so you can login with any username/password. You should be able to browser named resources and pre-view maps.
`https://<your external ip>/SpatialServerManager`
   
If you are using the OGC services please refer to the on-premise docs ([WFS](https://docs.precisely.com/docs/sftw/spectrum/24.1/en/webhelp/Spatial/Spatial/source/Resources/resources/repoman/wfs_settings.html), [WMS](https://docs.precisely.com/docs/sftw/spectrum/24.1/en/webhelp/Spatial/Spatial/source/Resources/resources/repoman/wms_settings.html), [WMTS](https://docs.precisely.com/docs/sftw/spectrum/24.1/en/webhelp/Spatial/Spatial/source/Resources/resources/repoman/wmts_settings.html)) to configure the Online resource / Service URL with the public access url (Ingress EXTERNAL-IP).


### [Next Step](enable-security.md)
