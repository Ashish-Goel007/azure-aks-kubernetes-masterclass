Cluster Autoscaler do not look at memory/CPU when it trigerrs the autoscaling of new nodes.

It looks at the unschedulable pods only

Cluster Autoscaler checks for unschedulable pods after every 10s. Once one or more unschedulable pods are detected by cluster autoscaler, it w
will run an algorithm to decide how many new nodes need to be provisioned to deploy new pending pods & what type of nodes should be provisioned.

Similarly, for every 10s, Cluster Autoscaler decides to remove the nodes only when the resource utilization goes below 50%

![image](https://github.com/Ashish-Goel007/azure-aks-kubernetes-masterclass/assets/35141714/db1f2ad0-4084-4deb-aa2a-3d70848214bc)
