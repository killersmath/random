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

Show pods with ip adress
```kubectl get pod -n namespace -o wide```

Find service ip maps
```kubectl get endpoints -n namespace```

Find ingress configuration
```kubectl get ingress -n namespace --watch```

## Services

An abstract way to expose an application running on a set of Pods as a network service. It means, the service is responsable to communicate with the pods.

The service is specificied to listen in one or more ports and forward it to the pod port.

ports:
  - protocol: TCP
    port: 3400 [Service Port]
    targetPort: 3700 [Pod Port]

It's important to remember, in case you need to communicate multi-ports in same service then each port must be named.

ports:
  - name: http
    protocol: TCP
    port: 80 [Service Port]
    targetPort: 80 [Pod Port]
  - name: https
    protocol: TCP
    port: 443 [Service Port]
    targetPort: 443 [Pod Port]

### Caracterstics
- Loadbalacing
- Stable IP address
- Loose coupling
  - Within & Outsie cluster

### Types
- ClusterIP
  - Default or Type: ClusterIP
  - Internal Port Access
  - Map the pod ports
- Headless:
  - Type: ClusterIP
  - Spec: ClusterIP: None
  - Internal Port Access
  - Specific Port
- NodePort
  - Type: NodePort
  - Port
    - nodePort: [30000,32767] in range
  - External Port (Direct Access)
- Load Balancer
  - Type: LoadBalancer
  - Port
    - nodePort: [30000,32767] in range
  - External Port (Acessable from LoadBalancer)
