### Pod, Replicaset and Deployment

### Pods
A pod is the smallest part of a cluster,with one or more containers
sharing the same resources such storage, network or namespaces
In production, pods are mostly deployed through templates using 
some workloads such as jobs, deployment or daemonset.

here is a sample of code to run a pod

```
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.14.2
    ports:
    - containerPort: 80

```

### ReplicaSet
Replicasets ensures a certain number of pods are running at a time
for example use the code below to create a 3 replicas of a frontend app

```
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: frontend
  labels:
    app: frontend
    tier: frontend
spec: 
  replicas: 3
  selector:
    matchLabels:
      tier: frontend
  template:
    metadata:
      labels:
        tier: frontend
    spec:
      containers:
      - name: nginx
        image: nginx

```

- copy and save the code as replicas.yaml
- use the command to apply ` kubectl apply -f replicas.yaml`

- validate with `kubectl get replicaset`, you notice a replicaset was created
  or `kubectl get rs`
- now validate pods `kubectl get pods`, this shows 3 pods
- try delete a pod with `kubectl delete pod <podname>`
- check pods again `kubectl get pods`
- you will notice a pod with STATUS 'creating' with few seconds AGE

### Deployments
Deployments are much more efficient ways of running pods, 
that involve replicas and other advanced integration, this are
more recommended in running production or dev workloads

for example

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80

```

- apply the deployment code, using the same steps as above
- to validate `kubectl get deploy`


