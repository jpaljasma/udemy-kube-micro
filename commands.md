
# Troubleshooting

## Switch kubectl config back to docker-desktop

Sometimes, the kubectl is configured for different context, and kubectl does not want to connect to your locally configured Docker Desktop.

`kubectl config current-context`

Start by printing out the list of all configured clusters:

`kubectl config get-clusters`
```
NAME
docker-desktop
gke_sre_4096_us-central1_dev
```

And then, switch to **docker-desktop** config to the correct context by running

`kubectl config use-context docker-desktop`

Now, running `kubectl version` will print out the expected output:

``` bash
% kubectl version

Client Version: v1.29.1
Kustomize Version: v5.0.4-0.20230601165947-6ce0bf390ce3
Server Version: v1.29.1
```

And we can verify by running

``` bash
% kubectl get all

NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   13m

