## Services Types
What are services
Service is a kubernetes component used to expose pods to the neccessary 
resource that need to consume it, a pod on its own has ip address in which
can be used to expose it, but due to instability of a pod a service is needed to 
expose it. This, in simple terms means, pods somtimes needs to restart or 
crash and recreated, which will have a different ip, we definately cannot keep track of 
these ip, especially when hundreds of pods is involved, this makes service 
our best option.

A service i.p doesnt change no matter the amount of times the pod crashes and 
get replaced.

there are 4 types are service:

- Nodeport: uses node ip to expose your app to the internet

- clusterIP: this is used for internal communication within the cluster

- Loadbalancer: This works better with cloud services exposing your application 
  through a loadbalancer

- ExternalIp: this is used for external resources usually cloud resources 
  like database connection on the cloud directly to your clusters without
  having the create pods for databases