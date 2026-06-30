# High Availability in Managed Kubernetes Clusters

## Overview
High Availability (HA) is a feature in managed Kubernetes clusters that ensures the control plane remains accessible and resilient to failures. When enabled, the Kubernetes key–value store (etcd) and other control plane components run across multiple nodes instead of a single node.

## What It Is
In a standard (non-HA) setup, the Kubernetes control plane—including the etcd database—runs on a single node. This creates a potential single point of failure: if that node becomes unavailable, the cluster cannot be managed.

With High Availability enabled, the control plane is distributed across multiple nodes. The etcd key–value store runs as a clustered system, replicating data across these nodes and using quorum-based consensus to maintain consistency.

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

## How to Enable or Disable
- **Enable HA**: Select the “High Availability” option during cluster creation. This deploys multiple control plane nodes with replicated etcd.
- **Disable HA**: Leave the option unselected. A single control plane node is used.

Note: This setting is typically fixed at creation time.

## Considerations
- **Cost**: Higher due to additional nodes
- **Reliability**: Eliminates single point of failure
- **Use Case**: Recommended for production; optional for dev/test

## Summary
High Availability improves cluster resilience by distributing the control plane across multiple nodes, ensuring continuous operation even when individual components fail.
