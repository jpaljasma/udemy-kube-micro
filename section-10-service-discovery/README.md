# Kubernetes Networking and Service Discovery

## Get all Namespaces

```bash
% kubectl get ns

NAME              STATUS   AGE
default           Active   5d20h
kube-node-lease   Active   5d20h
kube-public       Active   5d20h
kube-system       Active   5d20h
```

## Get all from Namespace

`kubectl get all -n kube-system --show-labels`

`kubectl describe svc kube-dns -n kube-system`

## Test with MySQL container

### Create MySQL service

`kubectl apply -f networking-tests.yaml`
`kubectl describe svc database`

### Connect from webapp

(Alpine Linux - no bash, thus we use just `sh`)
Note: using modern syntax here `kubectl exec [POD] -- [COMMAND] instead.`

`kubectl exec webapp-687b64b776-nlpbj -it -- sh`

#### Install MySQL client

```bash
% akp update
% apk add mysql-client
```


## Clean up

`kubectl delete svc database && kubectl delete pod mysql`