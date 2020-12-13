## ReplicaSet

Ensure specified number of pods replica are running at any time based on configuration that defined in spec file.

    ReplicaSet ---> API Server | ---> CLuster > Nodes > Pods (Pods specified by ReplicaSet)


When you submit ReplicaSet to API server then its upto API server, how schedule the pods. It is possible that a node can have multiple pods.

### Problem: 
Example: Requirement of deploying monitoring app at every node inside the cluster.

Answer: DaemonSet

## DaemonSet

* Ensure that all or some nodes inside the cluster run a copy of pod
* One Pod Per Node.
* As nodes are added to cluster, Pods are added 
* As nodes are removed from the cluster, those Pods are garbage collected
* Deleting a DaemonSet will clean up the pods it created

Use Cases:
- Node monitoring daemons. Ex: collected
- Log collection daemons. Ex: fluentd
- Storage daemons. Ex: ceph


## **Links**

- https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/
- https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/
- https://www.youtube.com/watch?v=yYeUic8B6fM&t=302s
