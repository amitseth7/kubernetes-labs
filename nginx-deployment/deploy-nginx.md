<link rel='stylesheet' href='../assets/css/main.css'/>

# Lab X.z - Deploy Nginx


## Overview



## Duration
15 minutes

## Step 1 - Prepare deployment file

create a folder called `nginx-deployment` on the master node and

```bash
$   mkdir -p  /home/ubuntu/k8/nginx-deployment
```

## Step 2 - Deployment file

get the [deployment file](deployment-nginx.yaml) and put it in the created folder

```bash
#Go to the created directory
$   cd /home/ubuntu/k8/nginx-deployment

#Download the yaml file
$   wget https://github.com/elephantscale/kubernetes-labs/blob/master/nginx-deployment/deployment-nginx.yaml
```

## Step 3 - Apply Deployment file

Apply the config files using `kubectl -apply` command

```bash
$   kubectl apply -f deployment-nginx.yaml
```

output will look like:
```console
deployment.apps/nginx-deployment created
```

## Step 4 - Verify pods
To verify that the pods are deployed and working properly execute the following command

```bash
$   kubectl get pods -o wide
```

output will look like:

```console
NAME                                READY   STATUS    RESTARTS   AGE     IP                NODE        NOMINATED NODE   READINESS GATES
nginx-deployment-7848d4b86f-8qtch   1/1     Running   0          4m39s   192.168.130.135   k-worker1   <none>           <none>
nginx-deployment-7848d4b86f-c4jj6   1/1     Running   0          4m39s   192.168.130.136   k-worker1   <none>           <none>
nginx-deployment-7848d4b86f-wj42l   1/1     Running   0          4m39s   192.168.130.134   k-worker1   <none>           <none>
nginx-deployment-7848d4b86f-xdmgc   1/1     Running   0          4m39s   192.168.130.137   k-worker1   <none>           <none>
```

**Note:** `IP`, `Node` and `Name` might be different for you but status must be `Running`.


## Well done! 👏

Your pods are up and running.

## References

- [https://kubernetes.io/docs/concepts/workloads/controllers/deployment/](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
- [https://unix.stackexchange.com/questions/49263/recursive-mkdir](https://unix.stackexchange.com/questions/49263/recursive-mkdir)
- [https://shapeshed.com/unix-wget/](https://shapeshed.com/unix-wget/)

---