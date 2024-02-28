# Microservice Architecture

## Easy cleanup of the existing services

We can delete the specific pods, replica sets, services and deployments by simply referring to the `yaml` file and calling

```bash
% kubectl delete -f workloads.yaml

service "fleetman-webapp" deleted
service "fleetman-queue" deleted
```

## Names are critical

Since services are referred to by their metadata name, it is critical to ensure the `metadata.name` is unique and what's expected by the application. I had quite a bit of digging to do when I named one of the services incorrectly, and the dependent service could not connect to it.