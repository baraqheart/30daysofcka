## Services Types
What are services
Service is a kuberneted component used to expose pods to the neccessary 
resource that need to consume it, a pod on its own has ip address in which
can be used to expose it, but due to instability of a pod a service is needed to 
expose it, this is simple terms means, pods somtimes needs to restart or 
crash and recreated will have a different ip, we deffinately cannot keep track of 
these ip, especially when hundreds of pods is involved, this makes service 
our best option.

A service i.p doesnt change no matter the amount of times the pod crashes and 
get replaced.

there are 4 types are service:

- Nodeport: 

- clusterIP: this is used for internal communication within the cluster

- Loadbalancer: 

- ExternalIp: this is   used to connect a database on the cloud
to your clusturs