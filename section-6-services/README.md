# Services in Kubernetes

https://kubernetes.io/docs/concepts/services-networking/service/

> "In Kubernetes, a Service is a method for exposing a network application that is running as one or more Pods in your cluster."

Pods come and go, but Services are long-lived in Kubernetes.

## Describe existing pods

```bash
% kubectl get all

NAME         READY   STATUS    RESTARTS   AGE
pod/webapp   1/1     Running   0          75m

NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   3h33m

% kubectl describe pod webapp

```

```
% kubectl apply -f webapp-service.yaml

service/fleetman-webapp created
```

```
% kubectl get all

NAME         READY   STATUS    RESTARTS   AGE
pod/webapp   1/1     Running   0          100m

NAME                      TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE
service/fleetman-webapp   NodePort    10.97.166.10   <none>        80:30080/TCP   7s
service/kubernetes        ClusterIP   10.96.0.1      <none>        443/TCP        3h58m
```

## Label matching

`app: webapp` labels should match in both Pod and Service definitions.
We will apply the changes to the existing folder that contains both pod and webapp

```bash
% kubectl apply -f .

pod/webapp configured
service/fleetman-webapp unchanged
```

By visiting http://localhost:30080/ in your browser, everything works as expected.

`kubectl get all --show-labels`

`kubectl get pods -o wide`

We can delete unused pod
`kubectl delete pod webapp`
