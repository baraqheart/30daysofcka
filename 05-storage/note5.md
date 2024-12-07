## STORAGES IN KUBERNETES
### Storage Class, Persistence Volume and Persistence Volume Claim
what are storage classes, persistent volumes and persistent volume claim

- Storage Class: defines how and what storage resources type are used to
  provisioned and managed storages in a cluster

- Persistent Volume: this is the resource that represents a piece of networked storage,   provisioned and managed by kubernetes

- Persistent Volume claim: is a request for storage resources, its a way for pod to request for storage from a persistent volume

**Note:**

In this project we explored both managed and custom defined storage classes

paying a close attention to storage.yaml, you'll notice two seperate pvc was defined with just one storage class, yes its correct. we trying to learn 2 different ways to use storage classes

i- custom-sc: this was a customly created storage class used in the custom pvc for the deployments

ii- managed-sc: eks by default provides storage classes by default, to check this on your cluster, run the command below

` kubectl get sc `

which can be used in your persistent volume claim configuration for your deployments

References:



above are some of the links, used to complete the project.

Remember to always check the documentation when writing your manifest files to avoid deprecated settings and errors

cheers!!!