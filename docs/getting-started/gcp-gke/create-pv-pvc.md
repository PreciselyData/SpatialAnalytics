## Create PV and PVC

A PV (Persistent Volume) is required to share files across all services (pods),
- File based Spatial data sets, such as Mapinfo TAB, Shape, GeoPackage and Geodatabase etc.
- Tile cache
- Map image cache
- Custom Symbols
- Extended DataProviders
- JDBC drivers
	
### Create a PVC/PV

We will use `standard-rwx` auto provisioner to provision a PV through a PVC. There are other provisioners that may give better overall performance.

Create a PVC that dynamically provisioning a PV using standard-rwx storage class,
```
kubectl apply -f ~/SpatialAnalytics/deploy/gcp-gke/pvc.yaml
```
Check results, the pvc status will become `Bound` after service pods are deployed.
```
kubectl get pvc
```

### [Next Step](prepare-repository-database.md)
