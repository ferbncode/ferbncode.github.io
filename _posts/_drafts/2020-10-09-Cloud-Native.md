---
layout: post
title:  "Kubernetes Pod Placement: Limits, Requests and Pod Priorities"
date:   20120-0206 09:30:00 +0530
tags: containers, kuberentes, requests, limits, note, diagram
p_tags: essay, diagram
meta:
    keywords: "diagrams, kubernetes, cloud native, microservices, requests"
---

An application's resource usage profile is dependent on a number of factors like the programming languages it uses (for instance, some compiled languages requiring less memory compared to interpreted and just-in-time runtimes), the business logic, it's dependencies and the actual implementation. Cloud-native environments like Kubernetes serve best for applications with a predictable demands and well defined runtime dependencies.

Resource usage of a pod (set of containers) during runtime influences it's scheduling, placement and it's eviction. Knowing the resource usage/demands for an application not only helps Kubernetes efficiently place it, but overall helps the administrators in **Capacity planning** (and 💰 allocation) of the complete cluster. In Kubernetes, other than resource usage, a number of other runtime dependencies like requirements of a specific kind of volume, requirement to bind to a port may influence the placement of a pod (if it is scheduled at all) and it's state (healthy or not). An example of a pod not being scheduled at all would be if the type of volume requested by the pod is not served by any of the nodes in the cluster node pool. 

> Compute resources in the context of Kubernetes are defined as something that can be requested by, allocated to, and consumed from a container.[1]

Resources can be compressible (like CPU, Network usage) which can be throttled temporarily if usage is exceeded or incompressible (like memory/disk), in which case evicting a pod is the only possible way to reclaim the exceeded usage. [2]

In the context of predictable demands for resource usage, Kubernetes provides two primitives to define on the `container` level: `limits` and `requests`. The `requests` detail is used to specify the minimum resources required and `limits` is for communicating the maximum permitted usage. 

#### Role in pod placement and eviction: `requests` and `limits`

1. While placing the pod, the scheduler considers only the nodes to accommodate minimum resource usage (`requests`) .
2. While evinction of a pod, there are certain rules. Based on the values in `requests` and `limits`, a pod is classified in below categories with increasing quality of service (QoS):
    - Best-Effort (No `requests` and `limits` specified)
    - Burstable (`requests` != `limits`)
    - Guaranteed (`requests` == `limits`)


#### Pod priority

Other than resource usage and runtime dependencies, `PriorityClass` in Kubernetes [3] is another player in pod placement and eviction and one of the tricky areas :D. 



References
* [1]:https://www.redhat.com/cms/managed-files/cm-oreilly-kubernetes-patterns-ebook-f19824-201910-en.pdf
* [2]: https://en.wikipedia.org/wiki/System_resource
* [3]: https://kubernetes.io/docs/concepts/configuration/pod-priority-preemption/