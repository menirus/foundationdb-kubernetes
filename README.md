# foundationdb-kubernetes
Goal: To deploy foundationdb cluster in kubernetes and to make it discoverable from outside the cluster

## Tried:
* Deployed single node foundationdb cluster in kubernetes cluster using NodePort service and exposing it using the kubernetes node's ExternalIP 
* Refer to NodePort directory for implementation details
* Refer https://github.com/menirus/fdb-server-docker for docker image details

## Next Steps:
* Use Ingress to deploy single node cluster
* Extend to multiple nodes
* Use StatefulSets for co-ordinators, storage nodes and TLogServers? What about PersistentVolumes?
* Test replication factors and resiliency of the cluster
* Explore if discovery can be done using hostname (probably by using a middleware for DNS lookup and giving the co-ordinator IPs?)
