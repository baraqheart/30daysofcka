### Health probe
There are 3 probes used to maintain the state and lifecycle of a pod,
each which its unique abilities should be used with great precaution

### LivenessProbe: 
kubelet uses this probe to know when to restart an applications that catch a
deadlock, this means when application starts and unable to make any progress.
Liveness probe is used to recover failed application but should be used with 
precaution as some application takes more time to load. 

### Readinessprobe: 
Kubelet uses this probe to know when a pod is ready to start accepting traffic,
when a pod is not ready, its endpoints are removed from service load balancer, this prevents. Unlike liveliness and startup probe, readiness probe runs through an application
lifecycle


### startupprobe:
This probe works only at startup, kubelet uses it to kno when an app starts,
until startup probe is completed none of the probes can run, this is to avoid 
interference with starting an app to avoid restarting slow loading apps.

### How to Configure Liveness, Readiness and Startup probe
There are 3 differrent ways to configure the 3 probe, Using:
  - commands
  - Http requests
  - TCP

**Define a liveness command**
  ```
  livenessProbe:
      exec:
        command:
        - cat
        - /tmp/healthy
      initialDelaySeconds: 5
      periodSeconds: 5
  ```
  
**Define a liveness http request**
 ```
  livenessProbe:
      httpGet:
        path: /healthz
        port: 8080
        httpHeaders:
        - name: Custom-Header
          value: Awesome
      initialDelaySeconds: 3
      periodSeconds: 3
 ```

**Define a TCP liveness**
 ```
 livenessProbe:
      tcpSocket:
        port: 8080
      initialDelaySeconds: 15
      periodSeconds: 10
 ```

