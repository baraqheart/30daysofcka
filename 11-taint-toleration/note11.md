### Taints and Toleration

Effects
- noSchedule : newer pods
- noExecute : existing and newer pods
- preferNoschedule : newer pods but not certain

kubectl taint node nodename gpu=true:Noschedule

 