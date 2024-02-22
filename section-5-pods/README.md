# Pods in Kubernetes

https://kubernetes.io/docs/concepts/workloads/pods/

Here's how to run the `first-pod.yaml`

```bash
% kubectl apply -f first-pod.yaml
pod/webapp created
```

```bash
% kubectl get all

NAME         READY   STATUS    RESTARTS   AGE
pod/webapp   1/1     Running   0          85s

NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   139m
```

## Verify that the pod is running

`kubectl describe pod webapp`

## Run a ls command against the pod

```
% kubectl exec webapp -- ls -latr

total 64
drwxr-xr-x    1 root     root          4096 Sep 11  2018 var
drwxr-xr-x    2 root     root          4096 Sep 11  2018 srv
drwxr-xr-x    2 root     root          4096 Sep 11  2018 sbin
drwx------    2 root     root          4096 Sep 11  2018 root
drwxr-xr-x    2 root     root          4096 Sep 11  2018 mnt
drwxr-xr-x    5 root     root          4096 Sep 11  2018 media
drwxr-xr-x    2 root     root          4096 Sep 11  2018 home
drwxrwxrwt    1 root     root          4096 Sep 26  2018 tmp
drwxr-xr-x    1 root     root          4096 Sep 26  2018 lib
drwxr-xr-x    1 root     root          4096 Jan  1  2023 usr
drwxr-xr-x    1 root     root          4096 Jan  1  2023 bin
dr-xr-xr-x   11 root     root             0 Feb 18 20:35 sys
drwxr-xr-x    1 root     root          4096 Feb 18 20:35 run
dr-xr-xr-x  231 root     root             0 Feb 18 20:35 proc
drwxr-xr-x    1 root     root          4096 Feb 18 20:35 etc
drwxr-xr-x    5 root     root           360 Feb 18 20:35 dev
-rwxr-xr-x    1 root     root             0 Feb 18 20:35 .dockerenv
drwxr-xr-x    1 root     root          4096 Feb 18 20:35 ..
drwxr-xr-x    1 root     root          4096 Feb 18 20:35 .
```

## SSH into a pod

`kubectl -it exec webapp -- sh`

### Install curl

```bash
apk update
apk upgrade
apk add curl
```

### Verify that the pod responds

`curl -v http://127.0.0.1/`
