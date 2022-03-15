# capi-templates-koord

## Differences between these templates and the default Cluster API templates

- Leverages ClusterResourceSet to deploy Calico for CNI
- Leverages ClusterResourceSet to deploy kube-vip for LoadBalancer services using BGP
- Uses kube-vip for Control Plane EIP management
- Configures cloud-provider-equinix-metal appropriately for kube-vip control plane management and load balancer services

## enabling CRS for CAPI

When deploying (or updating the management cluster):
```sh
export EXP_CLUSTER_RESOURCE_SET=true

clusterctl init --infrastructure packet
```

The Cluster API deployment can be updated manually post install if needed as well: https://cluster-api.sigs.k8s.io/tasks/experimental-features/experimental-features.html#enabling-experimental-features-on-existing-management-clusters

## Generating the templates

```sh
make generate
```
## Using the templates

For Cluster API v0.3.x:
```sh
export PROJECT_ID=<MY_PROJECT_ID>
export SSH_KEY=<MY_SSH_KEY_NAME>
CONTROLPLANE_NODE_TYPE=c3.small.x86 WORKER_NODE_TYPE=c3.small.x86 FACILITY=dc13 KUBERNETES_VERSION=1.22.4 clusterctl generate cluster --from ./cluster-template-v1alpha3.yaml capi-test
```

For Cluster API v1+:
```sh
export PROJECT_ID=<MY_PROJECT_ID>
export SSH_KEY=<MY_SSH_KEY_NAME>
CONTROLPLANE_NODE_TYPE=c3.small.x86 WORKER_NODE_TYPE=c3.small.x86 FACILITY=dc13 KUBERNETES_VERSION=1.22.4 clusterctl generate cluster --from ./cluster-template-v1beta1.yaml capi-test
```

## Updating various components properly

TODO