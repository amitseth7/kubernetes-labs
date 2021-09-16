<link rel='stylesheet' href='../../assets/css/main.css'/>

# Lab - Deploy Nginx


## Overview
On this lab, we are going to create a deployment with 4 pods, the image of this deployment is called `nginx-v1` after creating the original deployment, we will `rollout` to update the image to `nginx-v2`

## Duration
20 minutes


## Step-1: Deployment file

inspect  [deployment file](deployment-nginx.yaml)

## Step-3: Apply Deployment file

Apply the config files using `kubectl -apply` command

```bash
$   cd ~/kubernets-labs/rollout/1-nginx
$   kubectl apply -f deployment-nginx.yaml
```

output will look like:
```console
deployment.apps/nginx-deployment created
```

## Step-2: Expose

- expose the deployment
```bash
$ kubectl expose deployment nginx-deployment --port=80 --type=NodePort
```
output

```console
service/nginx-deployment exposed
```

- get nodeport
```bash
$  kubectl get service
```

output

```console
NAME               TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
kubernetes         ClusterIP   10.96.0.1       <none>        443/TCP        6m12s
nginx-deployment   NodePort    10.107.20.175   <none>        80:32073/TCP   54s
```

try to find the `NodePort` and open it using `http://MASTER-IP:PORT` in a browser

output will look like:

```console
Welcome to Webapp - v1
```

## Step-4: rollout an update

inspect v2 [deployment file](deployment-nginx-v2.yaml)

use the `v2` to update nginx from v1 to v2

```bash
$   cd ~/kubernets-labs/rollout/1-nginx
$   kubectl replace  -f deployment-nginx-v2.yaml
```

Notice that instead of `apply` we are using `replace`.

Monitor the status of rollout using the following command:

```bash
$  kubectl rollout status deployment nginx-deployment
```

output will look like:

```console
Waiting for deployment "nginx-deployment" rollout to finish: 3 out of 4 new replicas have been updated...
Waiting for deployment "nginx-deployment" rollout to finish: 3 out of 4 new replicas have been updated...
Waiting for deployment "nginx-deployment" rollout to finish: 3 out of 4 new replicas have been updated...
Waiting for deployment "nginx-deployment" rollout to finish: 3 out of 4 new replicas have been updated...
Waiting for deployment "nginx-deployment" rollout to finish: 1 old replicas are pending termination...
Waiting for deployment "nginx-deployment" rollout to finish: 1 old replicas are pending termination...
Waiting for deployment "nginx-deployment" rollout to finish: 1 old replicas are pending termination...
Waiting for deployment "nginx-deployment" rollout to finish: 3 of 4 updated replicas are available...
```

## Step-5: verify

open `http://MASTER-IP:PORT` in a browser, the output should be:

```console
Welcome to Webapp - v2
```



## Lab is Complete! 👏

