# General

- POD
  - Smallest unit
  - Created by deployment
- Replicaset
  - Resposable to handle the replicas of pods defined by eployment.
- Deployment
  - Blueprint for creating pods
  - Most basic configuration
    - Image
    - Storage
    - Initial commands
- Service
  - Resposable to handle the communication to pods
- Ingress
  - Resposable to handle the outside connection and forward to the services.

## Common commands

Show pods with ip address

```text
kubectl get pod -n namespace -o wide
```

Find service endpoints

```text
kubectl get endpoints -n namespace
```

Find ingress configuration

```text
kubectl get ingress -n namespace --watch
```
