## Namespces
Namespcaces are logical way of grouping kubernetes objects in a cluster, and can also be used
to define several properties of a group of resources such as networking, sucurity and resource 
management

By default most cluster have 4 namespaces, which are listed below:

to get the list of available namespces use the command

` kubectl get namespace `

- default: every newly created k8s objects is automatically assigned the default namespace, 
  when no namespace was specified during creation

- kube-node-lease: this is used to monitor node heartbeat lease used by kubelet to
  get node availability

- kube-public: this is namespace is publicly available to all users, it is mostly
  use to share configuration between namespaces

- kube-system: this namespace contains the controll plane components such as etcd, controller 
  manager, apiserver, and scheduler. these are managed by kubernetes

here is a way to check which api-resources is scoped at namespace level
` kubectl api-resources --namespaced==true `

for the cluster scoped level resources, the command below
` kubectl api-resources --namespaced=false `

### 1. How to create a new namespace and resource in the namespace
Therre are 2 different ways of creating a namespace
- Imperative method: usually a cli command
` kubectl create namespace dev `

this commands creates a dev namespace in our cluster, to view use

`kubectl get ns`

- Declarative method: this is a yaml file preconfigured, use the the command to apply

`kubectl apply -f namespace.yaml`

this creates a dev and prod namespaces a defined in the yaml file with the other con figuration

### 2.Namespace Networking
Namespace networking is the way objects from different namespaces commnunicate with
other objects in other namespace.

By default, objects are allowed to talk to other object from different workspace, 

- Example
dev-pod is a pod in the dev namespace 

prod-pod is a pod in prod namespace, we will try a curl, ping or telnet to understand better

pod.yaml is file to create both pod and service for dev and prod namespaces, now apply

 ``
`kubectl apply -f prod.yaml -n prod`
 `kubectl apply -f dev.yaml -n dev`

Lets log in to both pods and test connectivity
kubectl get po -n dev -o wide

` kubectl exec -it dev-pod -n dev -- sh `



` kubectl exec -it prod-pod -n prod -- sh `

Fully  qualified domain name is fqdn

` cat /etc/resolv.conf ` 

shows the fqdn, this works just fine when used to ping, curl 
or telnet other pod




### 3.Namespace resource management

limitsRange and ResourceQuota are used to manage resources in namespaces

- LimitsRange: is be used to enforce the amount of resources for each pods or container,  amount of storage for each pvcs and also enforce limits and requests ratio for a resource in a namespace

- ResourceQuota: defines the amount of resource allocated to an object in a namespace
   It can limit the quantity of objects that can be created in a namespace by type, as well as the total amount of compute resources that may be consumed by resources in that namespace
