# foundationdb-kubernetes
Goal: To deploy foundationdb cluster in kubernetes and to make it discoverable from outside the cluster

## Findings:
* For the cluster discovery, the co-ordinators should be exposed to the outside world from Kubernetes network using either NodePort Service, LoadBalancer Service or Ingress
* Deployed single node foundationdb cluster using NodePort service
* NodePort services run only in the ports in range 30000-32767
* FoundationDB internal implementations have a strict requirements on the port numbers, internal address and public address should both run in the same port. (hence changed default 4500 port to 31111)
* Also, --public-address should be accessible by the internet for the clients to connect. Let's say --public-address is local to the kubernetes cluster network but the same is exposed using a NodePort. If external client connects to the cluster, it says database unavailable and status says: "Unable to communicate with the cluster controller at 10.128.0.2:31111 to get status"  (which is the --public-address, local to kube network)


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
