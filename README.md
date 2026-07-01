# High Availability in Managed Kubernetes Clusters

High Availability (HA) is a feature in managed Kubernetes clusters that ensures the control plane remains accessible and resilient to failures. When enabled, critical components such as the Kubernetes key–value store (etcd) are deployed across multiple nodes to improve fault tolerance.

## Understanding High Availability
In a standard (non-HA) cluster setup, the Kubernetes control plane runs on a single node, consisting of the Kubernetes API server, key-value store, scheduler, and controller. This single node instance creates a potential single point of failure. If that node becomes unavailable, cluster management operations are disrupted.

With High Availability enabled, the control plane is distributed across multiple nodes. The etcd key–value store operates as a clustered system, replicating data between nodes and using quorum-based consensus to ensure consistency and reliability even if individual nodes fail.
## Architecture Diagram



+----------------------+
              |    Load Balancer     |
              +----------+-----------+
                         |
    -----------------------------------------
    |                    |                  |

+---------------+  +---------------+  +---------------+
| API Server 1  |  | API Server 2  |  | API Server 3  |
+---------------+  +---------------+  +---------------+
|                    |                  |
-----------------------------------------
|   etcd Cluster   |
|  (Key-Value DB)  |
+------------------+
(Quorum-based)

## What It’s Used For
The primary purpose of HA is to improve the reliability and uptime of Kubernetes clusters. It is especially important for:
- Production environments where downtime must be minimized
- Applications requiring high availability and fault tolerance
- Systems that need continuous access to the Kubernetes API

## How It Works
When HA is enabled:
- Multiple control plane nodes are provisioned
- The etcd key–value store is replicated across these nodes
- A load balancer distributes requests to the Kubernetes API servers
- The system continues functioning as long as a majority (quorum) of nodes are available

## Enable or Disable High Availability in Nebius AI Cloud
- **Enable HA**: Select the “High Availability” option during cluster creation. This deploys multiple control plane nodes with replicated etcd.
- **Disable HA**: Leave the option unselected. A single control plane node is used.

Note: This setting is typically fixed at creation time.
