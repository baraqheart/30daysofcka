### Authentication and Authorization
Note that this are two different things, despite the similarities

### Authentication
Authentication i used to ensures that only allowed users can  access a 
cluster securely.
There are 2 different types of users in kubernetes:
    - user
    - service account

### Authorization
Authorization is used to define, what tasks a user is eligible
to perform on what resource. By default, users are eligible to
perform alot of tasks, this might be a very bad practise to maintain
default configurations for users.

In kubernetes, there are several authorization modes used in granting 
requests, which can be any of these:

- AlwaysaAllow: poses high security threat and should only be used in
                testing environment
- AlwaysDeny: this mode blocks all requests
- ABAC: attribute based access control
- RBAC: role-based access control
- Node: grants permission to kubelet based on the pods schedules to run 
- Webhook: 

Considering the list of the authorization modes as listed above,
it is important to choose the appropriate mode for running secure
workloads in your cluster.

We will log in to the control plane server and locate the configuration 
file that have the authorization modes and we will make changes to this.

` $ docker exec -it cluster-app-project-control-plane bash`

` cd /etc/kubernetes/manifests`

![]()

It is also permitted to combine multiple modes in the configuration file

![]()

In the above screetshop, you will notice we have change the mode from
`Node,RBAC` to `AlwaysAllow,RBAC`. please note that RBAC does not have deny  
policy, and should neva be used with AlwaysAllow in production.

while some of the authorization modes are not within the scope of this course,
we will explore RBAC in the next chapter.
