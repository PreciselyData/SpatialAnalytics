## Prepare GKE cluster
Also see Google Cloud Document https://cloud.google.com/kubernetes-engine?hl=en

Note: a GKE Autopilot cluster is used in this doc. A Standard mode cluster can also be used but it has extra steps required that are not covered here.

### Create a GKE cluster

Set up the project and region to use, e.g. my-project, us-east1
```
gcloud config set compute/region us-east1
```
The project should be set automatically, but you can update it if needed,
```
gcloud config set project <my-project>
```
Check the settings,
```
gcloud config list
```

Create GKE cluster (autopilot) named spatial-cloud-native. You can specify different project and region with `--project` and `--region`.
```
gcloud container clusters create-auto spatial-cloud-native --region us-east1 --cluster-version 1.29.1
```
It may take few minutes to create the cluster. Wait until the command finished.
```
kubectl get nodes
```
You may see no resources at beginning as no pods deployed yet.
```
No resources found
```
Note: if the cluster version was not found, using the following command to list all valid cluster versions. Looking for one under REGULAR channel.
```
gcloud container get-server-config
```

### Install Ingress Controller (ingress-nginx)
First, add cluster admin permission:
```
kubectl create clusterrolebinding cluster-admin-binding \
  --clusterrole cluster-admin \
  --user $(gcloud config get-value account)
```
Then, install ingress controller:
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.10.0/deploy/static/provider/cloud/deploy.yaml
```
Find the external IP
```
kubectl get svc -n ingress-nginx
```
Looking for the EXTERNAL-IP from output. Wait a moment and try again if the EXTERNAL-IP is not assigned.
```
NAME                                 TYPE           CLUSTER-IP       EXTERNAL-IP     PORT(S)                      AGE
ingress-nginx-controller             LoadBalancer   34.118.225.23    34.23.192.143   80:31548/TCP,443:32362/TCP   21m
ingress-nginx-controller-admission   ClusterIP      34.118.232.254   <none>          443/TCP                      21m                                                                        443/TCP                      4h42m
```
The public access url would be like below. Try the url from your browser, you should see a 404 page from 'nginx'.
```
https://34.23.192.143
```

### Delete the GKE cluster
Once you finished the testing, if you do not want this cluster anymore, you can delete the cluster for cost saving,
```
gcloud container clusters delete spatial-cloud-native --region us-east1
```
verify and answer 'Y' to delete the cluster.


### [Next Step](create-pv-pvc.md)
