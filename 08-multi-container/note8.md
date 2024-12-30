
## Multi-containers

### Init-containers
this contianers are exepected to run once and complete execution successfully before the 
main container starts in the pod. A pod can have multiple init containers.
they usually are use to ensure or prepare the pod ready for other containers to
run properly.

Init containers supports resource management, this prevents init-containers 
from consuming the more than expected or allotcated resources.


### Sidecar
Init container complete its lifecycle before the main containers starts.
unlike init containers, sidecar containers supports all kind of probes
because they are secondary containers that runs alongside the main 
application container, sidecar container is also known as helper 
containers

sidecar containers are used to extend the functionality of the priamary container
such as monitoring, logging or security




### Application of different types of containers

coming soon