# Services

An abstract way to expose an application running on a set of Pods as a network service. It means, the service is responsable to communicate with the pods.

The service is specificied to listen in one or more ports and forward it to the pod port.

```yaml
ports:
  - protocol: TCP
    port: 3400 #[Service Port]
    targetPort: 3700 #[Container Port]
```

It's important to remember, in case you need to communicate multi-ports in same service then each port must be named.

```yaml
ports:
  - name: http
    protocol: TCP
    port: 80 #[Service Port]
    targetPort: 80 #[Container Port]
  - name: https
    protocol: TCP
    port: 443 #[Service Port]
    targetPort: 443 #[Container Port]
```

## Caracterstics

- Loadbalacing
- Stable IP address
- Loose coupling
  - Within & Outsie cluster

## Types

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
