Problem
The monitoring stack detected abnormal resource pressure after scaling the nginx workload. Some pods entered Pending state because the cluster reached its pod-per-node capacity.

Timeline
Deployment scaled to 12 replicas
Scheduler attempted to place pods
Nodes reached pod limit
Prometheus recorded CPU spike and scheduling pressure

Root Cause
The EKS node group initially contained only two worker nodes. Each node has a maximum number of pods determined by the AWS VPC CNI networking model. The monitoring stack plus the scaled application exceeded that limit.

Fix
The node group was expanded from two to three nodes, restoring scheduling capacity and allowing monitoring components to run normally.

Prevention
Implement cluster autoscaler or capacity alerts so the platform automatically adds nodes when scheduling pressure increases.