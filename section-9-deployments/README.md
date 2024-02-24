# Kubernetes Deployments

In Kubernetes, the Deployments is more sophisticated way of the ReplicaSet, and comes with a very important feature - an **automatic rolling updates** with zero downtime. It also allows you to do rollbacks in case something goes wrong.

## Monitor the status of the rolling deployment
`kubectl rollout status deployment.apps/webapp`

