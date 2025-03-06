### Taints and Toleration
**Taints** are used on nodes to prevent pods scheduled on them, this means a tainted
node will accept or might not accept any pod scheduled based on some certain condition

*there are different types of taint effect*

Effects
- noSchedule : applies to newer pods
- noExecute : existing and newer pods
- preferNoschedule : newer pods but not certain

- to taint a node, you will use the command below including the key value
of the condition

```yaml
kubectl taint node nodename gpu=true:Noschedule
```

- Tainted nodes can also be removed by adding a `-` to the end on command
 used to taint the node

```yaml
kubectl taint node nodename gpu=true:Noschedule-
```

**Tolerations** are used on pods to get its schedulling accepted by a node that
has been tainted depending on its the node's taint efect 

- to apply toleration to a pod, add this code to match the taint in the node 

 ```yaml
tolerations: 
- key: "gpu"
  operator: "Exists"
  effect: "NoSchedule"

  ```
 
 *OUTPUT*
```
USER@Baraqheart MINGW64 ~/Documents/devops_project/30daysofcka/11-taint-toleration 
$ kubectl describe node cluster-app-project-worker | grep -i taints
Taints:             gpu=true:NoSchedule

```

This was the result after taint was applied to a worker node on the cluster