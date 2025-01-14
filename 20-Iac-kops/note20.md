### Using KOPS

# Installing kops 
 - using linux, run the code

 ```
 curl -Lo kops https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64
 chmod +x kops
 sudo mv kops /usr/local/bin/kops
 ```

# Create cluster configuration
steps:
1. create an IAM user
2. setup the cli with `aws configure`
3. create an s3 bucket to store cluster state
4. export s3 bucket name and cluster name
5. create cluster with command

```
kops create cluster \
    --name=${NAME} \
    --cloud=aws \
    --zones=us-west-2a \
    --state=${BUCKET_NAME}

```

This is a simple configuration to implement kops cluster
If you have a need to configure dns services, refer to the kops documentation

### Commands in kops
- `kops create cluster ..`
- `kops update cluster ..`
- `kops delete cluster --name <clustername>`
- `kops get clusters`

[kops documentation](https://kops.sigs.k8s.io/getting_started/aws/)
[kops terraform configuration ](https://kops.sigs.k8s.io/terraform/)