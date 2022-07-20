A Keycloak (18.0.0+) is used for authentication and authorization. If you have an external Keycloak instance that can be accessed from inside the EKS cluster, then collect the issuer url for further service config, otherwise, you can deploy a keycloak service into the EKS cluster.


Deploy a Keycloak service into the EKS cluster.

Create a namespace for the Keycloak
$kubectl create ns keycloak


Identify the external loadbalancer host to expose the Keycloak Management Console UI
$kubectl get svc -n ingress-nginx

looking for the EXTERNAL-IP in the output
e.g. af5fd6acf60f747e492756edb9726215-e6f65bc2cad48f48.elb.us-east-2.amazonaws.com

Deploy keycloak by helm chart
$helm install keycloak spatial/keycloak-service --version 1.0.0-SNAPSHOT -n keycloak --set ingress.host=af5fd6acf60f747e492756edb9726215-e6f65bc2cad48f48.elb.us-east-2.amazonaws.com
Wait until keycloak-0 pod in keycloak namespace is up and ready (kubectl get pod -n keycloak)


Enable ingress class for keycloak
$kubectl -n keycloak annotate ingress keycloak kubernetes.io/ingress.class=nginx


Get the admin password (like 'V4YAGs76OzGMvA==')
$kubectl -n keycloak get secret credential-spatial-keycloak -o=jsonpath="{.data.ADMIN_PASSWORD}" | base64 -d

    
Open a browser and login to keycloak console with the admin credentials at
https://af5fd6acf60f747e492756edb9726215-e6f65bc2cad48f48.elb.us-east-2.amazonaws.com/auth/admin


Create a realm for spatial services

Import realm-spatial.json to create the realm.
In administration console, move cursor over the 'Master' realm and click on 'Add realm'

Select the realm file 'realm-spatial.json', give a name to the new realm (use all lowercase name, e.g. development) and click the 'Create'.

also see Keycloak document about the Management Console. https://www.keycloak.org/docs/latest/server_admin/


Update service config to use the keycloak

$kubectl edit cm spatial-config -n spatial

oauth2.enabled: "true"
oauth2.issuer-uri: "http://keycloak-discovery.keycloak.svc.cluster.local:8080/auth/realms/<your realm name>"
oauth2.client-id: "spatial"
oauth2.client-secret: "fd17bc1d-cefc-41a3-8c50-bb545736caa6"
spring.security.oauth2.client.provider.keycloak.issuer-uri: "http://keycloak-discovery.keycloak.svc.cluster.local:8080/auth/realms/<your realm name>"
  

Restart all services to pick up the config
$kubectl rollout restart deployment -n spatial
$kubectl get pod -n spatial

Login to Spatial Manager when all services are ready. Initial password for admin is 'Spatialadmin0'
https://af5fd6acf60f747e492756edb9726215-e6f65bc2cad48f48.elb.us-east-2.amazonaws.com/SpatialServerManager

Verify if you can preview a map in Spatial Manager.