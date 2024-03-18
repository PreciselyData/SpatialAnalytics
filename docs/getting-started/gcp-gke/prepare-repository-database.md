## Prepare database for repository

A MongoDB replica set is used to persistent repository content. 

For a production deployment, a multi-node MongoDB replica set is recommended. Here is the link to [Install MongoDB](https://www.mongodb.com/docs/manual/installation/)


If you have a MongoDB replica set that can be accessed from inside the Kubernetes cluster, then collect the connection url for further service config.

If you don't have a MongoDB replica set currently, for your convenience, you can deploy a single node MongoDB replica set for testing by the first step below, otherwise, go to the next step.

### Install a MongoDB instance by helm for testing

Install MongoDB from helm chart
```
helm install mongo charts/mongo-standalone -n mongo --create-namespace
```
```
kubectl get pod -n mongo
```
Wait until the mongo pod is ready
```
NAME                                      READY   STATUS    RESTARTS   AGE
mongo-XXXXXXXXXX-XXXX                     1/1     Running   0          8m35s
```
This will install a single node replica set instance without authentication
```
connection uri = mongodb://mongo-svc.mongo.svc.cluster.local/spatial-repository?authSource=admin&ssl=false
```

### [Next Step](deploy-spatial-services.md)
