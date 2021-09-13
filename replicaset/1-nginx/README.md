<link rel='stylesheet' href='../../assets/css/main.css'/>

# Lab - Deploy Nginx


## Overview
On this lab you will learn how to create replicasets to manage your pods and scale up/down them horizontally.


## Duration
35 minutes


## Step 1 - replicaset file

inspect  [replicaset file](replicaset-nginx.yaml)

## Step 2 - Apply replicaset file

Apply the config files using `kubectl -apply` command

```bash
$   cd ~/kubernets-labs/replicaset/1-nginx/
$   kubectl apply -f replicaset-nginx.yaml
```

output will look like:
```console
replicaset.apps/nginx-replicaset created
```

## Step 3 - Verify pods
To verify that the pods are deployed and working properly execute the following command

```bash
$   kubectl get pods -o wide
```

output will look like:

```console
NAME                     READY   STATUS    RESTARTS   AGE   IP                NODE        NOMINATED NODE   READINESS GATES
nginx-replicaset-7w2f2   1/1     Running   0          48s   192.168.130.149   k-worker1   <none>           <none>
nginx-replicaset-8cbpx   1/1     Running   0          48s   192.168.82.139    k-worker2   <none>           <none>
nginx-replicaset-c72fq   1/1     Running   0          48s   192.168.130.148   k-worker1   <none>           <none>
nginx-replicaset-wpxs9   1/1     Running   0          48s   192.168.82.140    k-worker2   <none>           <none>
```

**Note:** `IP`, `Node` and `Name` might be different for you but status must be `Running`.

## Step 4 - Describe

check your replicaset configuration

```bash
$ kubectl describe replicaset nginx-replicaset
```

output will look like:

```console
Name:         nginx-replicaset
Namespace:    default
Selector:     app=nginx
Labels:       <none>
Annotations:  <none>
Replicas:     4 current / 4 desired
Pods Status:  4 Running / 0 Waiting / 0 Succeeded / 0 Failed
Pod Template:
  Labels:  app=nginx
  Containers:
   nginx:
    Image:        nginx
    Port:         80/TCP
    Host Port:    0/TCP
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Events:
  Type    Reason            Age   From                   Message
  ----    ------            ----  ----                   -------
  Normal  SuccessfulCreate  109s  replicaset-controller  Created pod: nginx-replicaset-8cbpx
  Normal  SuccessfulCreate  109s  replicaset-controller  Created pod: nginx-replicaset-c72fq
  Normal  SuccessfulCreate  109s  replicaset-controller  Created pod: nginx-replicaset-wpxs9
  Normal  SuccessfulCreate  109s  replicaset-controller  Created pod: nginx-replicaset-7w2f2
```
## Step 5 - scale up/down

to scale up/down your replicaset use the following command

```bash
$ kubectl scale --replicas=8 replicaset nginx-replicaset
```

to verify get list of all pods

```bash
$   kubectl get pods -o wide
```

result:

```console
NAME                     READY   STATUS    RESTARTS   AGE     IP                NODE        NOMINATED NODE   READINESS GATES
nginx-replicaset-68wtd   1/1     Running   0          64s     192.168.130.153   k-worker1   <none>           <none>
nginx-replicaset-7w2f2   1/1     Running   0          4m58s   192.168.130.149   k-worker1   <none>           <none>
nginx-replicaset-8cbpx   1/1     Running   0          4m58s   192.168.82.139    k-worker2   <none>           <none>
nginx-replicaset-c72fq   1/1     Running   0          4m58s   192.168.130.148   k-worker1   <none>           <none>
nginx-replicaset-f5d7t   1/1     Running   0          64s     192.168.130.150   k-worker1   <none>           <none>
nginx-replicaset-f7j4r   1/1     Running   0          64s     192.168.130.152   k-worker1   <none>           <none>
nginx-replicaset-sj24m   1/1     Running   0          64s     192.168.130.151   k-worker1   <none>           <none>
nginx-replicaset-wpxs9   1/1     Running   0          4m58s   192.168.82.140    k-worker2   <none>           <none>
```

**Note:** `IP`, `Node` and `Name` might be different for you but status must be `Running`.


## Step 6 - Remove the replicaset

Using `kubectl remove replicaset` you can remove your replicaset

```bash
$ kubectl delete replicaset nginx-replicaset
```

output will look like:

```console
replicaset.apps "nginx-replicaset" deleted
```

## Well done! 👏