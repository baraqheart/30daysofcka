### Prerequisite
- create the cluster using kind, there are 2 different ways to create a cluster. 

i. imperative way

```yaml
kind create cluster 
```

ii. declarative eay

```
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
- role: worker
- role: worker
```

note: kind cluster donot expose ports external by default, hence we add these codes to the control plane section of the kind cluster creation code

```
extraPortMappings:
  - containerPort: 80
    hostPort: 80
    listenAddress: "0.0.0.0" # Optional, defaults to "0.0.0.0"
    protocol: udp # Optional, defaults to tcp
```

- lets, apply the kind.yaml file to create our cluster

```yaml
kind create cluster --config kind.yaml --name cluster-app-project

```

iii. clean up

Delete idle clusters, when you are done with your project to 
free up space

` kind delete cluster --name  clusterk`

you can also get the list of running cluster, using the command
below

` kind get clusters`