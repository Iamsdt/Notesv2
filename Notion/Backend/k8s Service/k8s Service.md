---
Created by: Shudipto Trafder
Created time: 2024-01-09T22:24
Last edited by: Shudipto Trafder
Last edited time: 2024-01-09T22:39
tags:
  - k8s
---
A Service in Kubernetes is an abstraction which defines a logical set of Pods and a policy by which to access them. Services enable a loose coupling between dependent Pods.

The set of Pods targeted by a Service is usually determined by a _label selector_ (see below for why you might want a Service without including a `selector` in the spec).

  

Services allow your applications to receive traffic. Services can be exposed in different ways by specifying a `type` in the spec of the Service:

- _ClusterIP_ (default) - Exposes the Service on an internal IP in the cluster. This type makes the Service only reachable from within the cluster.
- _NodePort_ - Exposes the Service on the same port of each selected Node in the cluster using NAT. Makes a Service accessible from outside the cluster using `<NodeIP>:<NodePort>`. Superset of ClusterIP.
- _LoadBalancer_ - Creates an external load balancer in the current cloud (if supported) and assigns a fixed, external IP to the Service. Superset of NodePort.
- _ExternalName_ - Maps the Service to the contents of the `externalName` field (e.g. `foo.bar.example.com`), by returning a `CNAME` record with its value. No proxying of any kind is set up. This type requires v1.7 or higher of `kube-dns`, or CoreDNS version 0.0.8 or higher.

  

## **Services and Labels**

A Service routes traffic across a set of Pods. Services are the abstraction that allows pods to die and replicate in Kubernetes without impacting your application. Discovery and routing among dependent Pods (such as the frontend and backend components in an application) are handled by Kubernetes Services.

![[module_04_labels.svg]]