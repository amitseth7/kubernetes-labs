<link rel='stylesheet' href='../assets/css/main.css'/>

# Lab - Service manifest


## Overview

In this lab you will how to create a service and access your cluster using that service.


## Duration
20 minutes


## Step 1 - Dependency

This lab depends on [deploy lab](../deployments/1-nginx/)

deploy the lab, but don't delete it.

## Step 1 - manifest file

inspect  [service file](service-nginx.yaml)

## Step 3 - Apply service file

Apply the config files using `kubectl apply` command

```bash
$   cd ~/kubernets-labs/service-nginx
$   kubectl apply -f service-nginx.yaml
```

output will look like:
```console
service/nginx-service created
```

## Step 4 - get list of services

run the following command to get list of services on your cluster

```bash
$ kubectl get services
```

output will look like:

```console
NAME            TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)          AGE
kubernetes      ClusterIP   10.96.0.1     <none>        443/TCP          5d5h
nginx-service   NodePort    10.99.46.93   <none>        8080:30007/TCP   61s
```

## Step 4 - access cluster

open a browser and open any of the nodes in the cluster with port `30007`

```bash
http://nodeIP:30007/
```
output should look like:

![](pf.jpg)



## Step 5 - Delete services

Use the following command to delete your service;

```bash
kubectl  delete service nginx-service
```

output

```console
service "nginx-service" deleted
```


## Well done! 👏
