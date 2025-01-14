### static pods, nodename, labels and  nodeSelector, manual scheduling

At this point, we are well informed that scheduler is responsible 
in schedulling newly created pods to nodes with the required 
resources to run the pods. 

If we try to get all the pods running on kube-system namespace, 
we will find all the control plane components running as pods,
this leaves us to wonder if scheduler is also responsible for that.

### static pods
static pods are used in all control plane components, this ensures 
scheduler does not manage this types of pods. 

Static Pods are always bound to one Kubelet on a specific node.

### Manual Schedulling 
- nodename

- nodeSelector



coming soon