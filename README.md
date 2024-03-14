<h1 align="center">Spatial Analytics</h1>

<p align="center">
  <img src="Precisely_Logo.png" alt="precisely-logo"/>
  <br>
  <i>Spatial Analytics is the name for our existing Spectrum Spatial product, designed to deploy to 
      <br>cloud native (Kubernetes) architectures.</i>
  <br>
</p>

<p align="center">
  <a href="https://www.precisely.com"><strong>www.precisely.com</strong></a>
  <br>
</p>
<hr>


## Benefits of cloud native deployment
### Flexibility of deployment
Spatial services are delivered as separate microservices in multiple Kubernetes pods using container-based delivery. Containers are orchestrated by Kubernetes with efficient distribution of workloads across a cluster of computers.

### Elastic scaling and clustering
Scale according to use cases (for example environments can scale up for overnight tile caching, scale up to meet application usage during the day). Autoscaling or manual scaling via command line or K8s dashboard. Major APIs such as Mapping, Tiling and Feature services can be separately scaled to match requirements.

### High availability
Kubernetes handles pod health checks and ensures cluster is resilient for mission critical cases, providing auto failover. K8s monitoring tools for health and availability and server resource usage.

### Automatic rollbacks & rollouts
Deployed from container registry. Ease of deployment and upgrades. Kubernetes can progressively roll out updates and changes to your app or its configuration. If something goes wrong, Kubernetes can and will roll back the change.
Optimised infrastructure costs: Scale for usage rather than maximum anticipated capacity. Pricing model will reflect usage, hence cost of ownership can be reduced to match actual demand.

### Portability
Can be deployed on premise or to a cloud provider. Portability and flexibility in multi-cloud environments.

## Documentation

- [Getting Started AWS](docs/getting-started/aws-eks/README.md)
- [Getting Started AZURE](docs/getting-started/azure-aks/README.md)
- [Getting Started Google Cloud](docs/getting-started/gcp-gke/README.md)