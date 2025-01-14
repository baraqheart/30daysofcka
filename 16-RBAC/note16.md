# RBAC Role Based 

We have seen, how to create users and issue certificates to user and more.
In this chapter, we will explore more about authorization

There are 4 major concepts in this part, of which are:
1. roles
2. role-binding
3. clusterrole
4. clusterrole-binding

# Roles
Roles are used to grant permissions within a namespace

For example: baraqheart is a developer who recently joined the teamX, she is only allowed to create, and list the pods and services in the staging namespace. Here is the configuration file to enforce this rule.

```
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: staging
  name: pod-svc
rules:
- apiGroups: [""] 
  resources: ["pods","services"]
  verbs: ["create","get", "watch", "list"]
```

# Role-binding
Role-binding uses roles to set permissions on a user or set of users. there are 3 different types of users that can be used in a role;
- user
- group
- service account


# Clusterrole-binding
Clusterrole on the other hand can be used to set permissions within a namespace, accross all namespaces and cluster scoped resources such as nodes













References
[rbac](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)