 # Certificate
certificate are used to ensure secure communication in a kubernetes cluster,


The cycle of generating a certificate, starts from a user generating private key 
in other to request for csr certificatesigningrequest, which needs to be approved before it can be signed.

Please note that, in other to be able to perform these task each user designated to or eligible to perform these tasks are required some permissions to perform 
the tasks, read the csr to have a full understanding of the rbac [rbac rules](https://kubernetes.io/docs/reference/access-authn-authz/certificate-signing-requests/)

 ### Generating certificates manually 
 When using client certificate authentication, you can generate certificates manually through easyrsa, openssl or cfssl

 TLS is a protocol that encrypts and authenticates data between web applications and servers. Certificates are used to authenticate over tls

we will use openssl, for this project 

### Steps 

1. generate a private key 

```
openssl genrsa -out baraqheart.key 2048
```

2. generate a public key, using the private key created in step 1
   this produces a csr file

```
openssl req -new -key baraqheart.key -out baraqheart.csr -subj "/CN=baraqheart"`
```

3. create a certificate signing request
- you can encode the csr key using the command below and copy it to the csr yaml file    `$(cat baraqheart.csr | base 64 | tr -d "\n" )` 

- or use the command directly in the .spec.request section 

```
apiVersion: certificates.k8s.io/v1
kind: CertificateSigningRequest
metadata:
  name: myuser
spec:
  request: $(cat baraqheart.csr | base 64 | tr -d "\n" )
  expirationSeconds: 86400  # one day
  usages:
  - client auth

```
- save the code as csr.yaml and apply
- to validate ` kubectl get csr `

4. Get the csr to be approve, this should be done by an admin
  
  in the next chapters we will learn RBAC  role based access control
  this will be able to restrict who is able to approve and sign a certificate

  ` kubectl certificate approve baraqheart `

5. To retrieve the certificate from the csr

  ` kubectl get csr/myuser -o yaml `

6. Export the issued certificate from the csr

` kubectl get csr myuser -o jsonpath='{.status.certificate}'| base64 -d > myuser.crt `


7. create role and rolebinding for user
`kubectl create role dev --verb=create --verb=get --resource=pod  `
` kubectl create role-binding dev-user --role=dev --user=baraqheart `

8. Add context and user to the kubeconfig file
  - 
  ` kubectl config set-credentials baraqheart --client-key=baraqheart.key --client-certificate=baraqheart.crt --embed-certs=true `
  
  - define context for user on app1cluster
  ` kubectl config set context b-app1cluster --cluster=app1cluster --use= baraqheart `

  - get the list of contexts

  ` kubectl get contexts `

  - to use the context
   
   ` kubectl use context b-app1cluster `
 Reference
 [manual certificate docs](https://kubernetes.io/docs/tasks/administer-cluster/certificates/)

 [certificate signing request](https://kubernetes.io/docs/reference/access-authn-authz/certificate-signing-requests/)

 [tls](https://kubernetes.io/docs/tasks/tls/managing-tls-in-a-cluster/)

