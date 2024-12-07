### Configuration management
there are are 2 major objects for setting configurations in kuberntes
- Secret
- configmap

- Secret: is used when sentitive data are involved, and available
to pods as variabple or volume

i. create a filename secret.yaml and copy below text in to it

```
apiVersion: v1
kind: Secret
metadata:
  name: pod-secret
data: 
  password: slfjvnc==
  token: jdgbjgndsdmdjdk==

```

note that secret data are encoded in base64, here is how to 
make your sensitive data be encoded in base64

` echo -n "mypassword" | base64 `

now apply witih `kubectl apply -f secret.yaml`

ii. create a pod, or deployment and insert secret in to the env part
of the container

```
env: 
- name: pass
  valueFrom:
    secretKeyRef:
      name: pod-secret
      key: password
```


- configmap: is used when the details involved is not sensitive data, 
this will be available to pod to consume as variables or volumes.
example below is a file used to create configmap

iii. create a file configmap.yaml and copy code below

```
apiVersion: v1
kind: configMap
metadata:
  name: pod-configmap
data: 
  endpoint: localhost
  

```

iv. insert configmap in to the env part of the container

```
env: 
- name: endpoint
  valueFrom:
    configMapKeyRef:
      name: pod-secret
      key: password

```

this is how to read configmap and secret in to a pod or deployment