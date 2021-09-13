<link rel='stylesheet' href='../../assets/css/main.css'/>

# Lab - Deploy Nginx


## Overview



## Duration
15 minutes

## Step 1 - Prepare deployment file

create a folder called `nginx-deployment` on the master node and

```bash
$   mkdir -p  ~/kubernets-labs/nginx-deployment
```

## Step 2 - Deployment file

inspect  [deployment file](deployment-nginx.yaml)

## Step 3 - Apply Deployment file

Apply the config files using `kubectl -apply` command

```bash
$   cd ~/kubernets-labs/nginx-deployment
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

## Step 5 - Describe

check your deployment configuration

```bash
kubectl describe deployment nginx
```

## Step 6 - Remove the deployment

Using `kubectl remove deployment` you can remove your deployment

```bash
$ kubectl delete deployment nginx-deployment
```

## Well done! 👏

Your pods are up and running.

## References

- [https://kubernetes.io/docs/concepts/workloads/controllers/deployment/](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
- [https://unix.stackexchange.com/questions/49263/recursive-mkdir](https://unix.stackexchange.com/questions/49263/recursive-mkdir)
- [https://shapeshed.com/unix-wget/](https://shapeshed.com/unix-wget/)

---