# High Availability in Managed Kubernetes Clusters
This article describes the High Availability feature that Nebius AI Cloud provides for managed Kubernetes clusters.

## What is High Availability?
High Availability (HA) is a feature in managed Kubernetes clusters that ensures the control plane remains accessible and resilient to failures. When enabled, critical components such as the Kubernetes key–value store (etcd) are deployed across multiple [nodes][control-node] to improve fault tolerance.

> **Note**: For more information on the control plane and how it manages Kubernetes cluster status, see [Kubernetes Control Plane Components][control-plane].

## How High Availability Works
In a standard (non-HA) cluster setup, the Kubernetes control plane runs on a **single node**, consisting of the Kubernetes API server, [key-value store][etcd-db], [scheduler][kube-scheduler], and [controller][kube-controller]. This node instance creates a potential single point of failure if it becomes unavailable, disrupting cluster management operations.

With High Availability enabled, 
- The control plane is distributed across **multiple nodes**
- The etcd key–value store operates as a clustered system, replicating data across multiple nodes
- A load balancer distributes requests from worker nodes (Virtual Machines) to the Kubernetes API servers
- The system continues functioning as long as a majority ([quorum][quorum-consensus]) of nodes are available

This type of cluster architecture ensures consistency and reliability even if individual nodes fail.

<p align="center">
<img width="800" height="800" alt="High Availability Architecture" src="images/High%20Availability%20Architecture.png">
</p>

## Typical Use Cases of High Availability
The primary purpose of HA is to improve the reliability and uptime of Kubernetes clusters. Some of the important use cases include:
- Production environments where downtime must be minimized
- Applications requiring high availability and fault tolerance
- Systems that need continuous access to the Kubernetes API

## Enable or Disable High Availability in Nebius AI Cloud
In the **Create Managed Kubernetes® cluster** dialog box, navigate to the **Control plane** section and perform one of the following actions based on your preference:
- **Enable HA**: Select the **High Availability** option during cluster creation. This deploys multiple control plane nodes with replicated etcd.
- **Disable HA**: Leave the option unselected. A single control plane node is used.

<p align="center">
<img width="370" height="450" alt="Create Kubernetes Managed Cluster" src="images/Create%20Kubernetes%20Managed%20Cluster.png">
</p>

> **Note**: This setting is typically configured during cluster creation and may not be editable after the cluster is deployed. Make sure to verify that before completing cluster creation.

[control-plane]: https://kubernetes.io/docs/concepts/architecture/#control-plane-components "Control Plane Components"
[etcd-db]: https://kubernetes.io/docs/concepts/architecture/#etcd "etcd Database Store"
[kube-scheduler]: https://kubernetes.io/docs/concepts/architecture/#kube-scheduler "Control Plane Scheduler"
[kube-controller]: https://kubernetes.io/docs/concepts/architecture/#kube-controller-manager "Kubernetes Controller Manager"
[control-node]: https://kubernetes.io/docs/concepts/architecture/nodes/ "Worker Node VM"
[quorum-consensus]: https://milvus.io/ai-quick-reference/what-is-a-quorum-in-distributed-databases "Quorum in Distributed Databases"
