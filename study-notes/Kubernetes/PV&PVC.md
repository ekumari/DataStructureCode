## Storage Volume

Q. How can data persist  through-out lifecycle of pod?
Q. How can data persist beyond lifecycle of pod?
Q. How can containers share files between containers in pod?

## Volumes: Directory with some data in it

*   Pods are stateless
*   Volume bring persistence to pods

Adv. of k8s volumes vs Docker volumes
*   Container(s) has access to volume.
*   Volumes are associated with Lifecycle of pod
*   Support many types of volumes
    -   Ephemeral: same lifetime as  pods
    -   Durable: beyond pods lifetime, data persisted even after pod lifetime
    There are cloud based volume: awsElasticBlockStore
              host based volume: emptyDir
              network based: nfs

EmptyDir, hostPath and gcePersistentDisk

## EmptyDir
*   Creates empty directory first when a pod is assigned to node
*   Stay as long as pod is running
*   Once pod is removed from a node, emptyDir is deleted forever
Use Cases:
-   Temporary space

## hostPath
*   mounts a file or directory from host node's filesystem into your pod(hostPath is attached to node so if pod recreate in the same node then it can reuse the volume)
*   Remains even after the pod is terminated
*   Similar to docker volume
*   Data remain even after pod is deleted

## GCEPERSISTENT DISK

* Volume mounts a Google compute engine(GCE) Persistent Disk into pod
* Volume data is persisted even after pod terminations.
* Read-write only on one node and Read-write on many nodes.



## Persistent Volumes (PV & PVC)

PV: Persistent Volume

    - Piece of pre-provisiond storage in Cluster
    - Data in it exist beyond the lifecyle of pod

Lifecyle of Persistent Volume:
1. Provisioning: Admin creates a storage chunks/volume.. these volume can be any storage type such as block, nfs, distributed.. (called as PV)

    Provisioning done by 1. Static 2. Dynamic
2. Binding: Bind the storage request to the persistent volume (that was provisioned earlier state) - called as PVC

3. Using
4. Reclaiming: when user is done with volume, they can delete the volume and claim the volume

PVC: Persistent Volume Claim

    - Developer Request for storage of some capacity along with some access mode such as read-write or read only
    
Provisioning has 2 types:
- Static: PV needs to created before PVC (PersistentVolume create then PVC)
- Dynamic: PV is created at the time of PVC (StorageClass create then PVC)