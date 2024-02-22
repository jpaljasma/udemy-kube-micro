# Installing ActiveMQ

## Troubleshooting

http://localhost:30010/ may not always open due to some sort of bug. To fix that, run a port forwarding in a Terminal window (keep it open):

`kubectl port-forward svc/fleetman-queue 30010:8161`

## Apply all files

`kubectl apply` only allows to apply one file at a time, and that can be super inconveniet when dealing with multiple files. If you have organized all your yaml files in a folder, you can just apply `.` for entire folder

```bash
% kubectl apply -f .

pod/webapp unchanged
pod/webapp-release-0-5 unchanged
pod/queue unchanged
service/fleetman-webapp unchanged
service/fleetman-queue configured
```
