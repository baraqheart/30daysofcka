## Daemonset, jobs and cronjobs

### Daemonset
A DaemonSet can be used to ensure that all eligible nodes
run a copy of a Pod, this involves pods that provide tasks
such as monitoring, logging networking and more


### Job
This is used for a one off tasks for deploying one or more pods, 
job is similar to cronjob. it doesnt include a scheduling 
option when deploying

### CronJob
Cronjob is a way of running a single or multiple pods 
that runs regularly or based on schedule 

```
apiVersion: batch/v1
kind: CronJob
metadata:
  name: hello
spec:
  schedule: "* * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: hello
            image: busybox:1.28
            imagePullPolicy: IfNotPresent
            command:
            - /bin/sh
            - -c
            - date; echo Hello from the Kubernetes cluster
          restartPolicy: OnFailure

```

# ┌───────────── minute (0 - 59)
# │ ┌───────────── hour (0 - 23)
# │ │ ┌───────────── day of the month (1 - 31)
# │ │ │ ┌───────────── month (1 - 12)
# │ │ │ │ ┌───────────── day of the week (0 - 6) (Sunday to Saturday)
# │ │ │ │ │                                   OR sun, mon, tue, wed, thu, fri, sat
# │ │ │ │ │ 
# │ │ │ │ │
# * * * * *

Emphasis on the schedule (* * * * * *) this means every minutes, job should run
 
 30 * * * * this means every 30 minutes, task should be performed

 0 2 * * * this means schedule this task to run every 2am daily

 0 5 * 3,6,9,12 * this means, task occurs at 5am quarterly
