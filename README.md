# Setting Limits to your Linux Containers

You should be setting limits to your containers! I know the internet is full of quotes linking “setting limits” to uncreative attitude and bounderies to innovation, there is a known expression in my country; “Brazilians has no limits” to illustrate the curious and creative ways we use to solve problems in face of limitations, but we will see in this article that when it comes to Linux containers, it’s actually important to set resource limits.

By default there is no any mechanisms avoiding your containers to consume the all the memory available in your host, if a process is allowed to consume unlimited resources in your container, your cluster can quickly run out of Memory and CPU, disrupting your deployment thereby starving legitimate
applications. 

### In this article I will show you:

*	Setting limits to your containers is important.
*	Setting resource limits in Kubernetes. 
*	Implementing limits to your Containers and Pods in Fargate.
*	Setting Memory And CPU Limits In Docker.



### Setting limits to your containers is important

By setting resource limits to your containers, you protect your environment to from attacks like [resource exhaustion attack](https://en.wikipedia.org/wiki/Resource_exhaustion_attack), improve efficiency in resources utilization, promote a more efficient resource allocation, and minimize costs. 

By applying limits to resource utilization for your containers you also improves visibility on how much memory and CPU the conainer process is demanding from the host operation system. In the Sysdig 2022 Cloud‑Native Security and Usage Report Sysdig shared some interesting finds based on the data gattered from the billions of containers their customers run over the course of a year and the ammount of workloads that does not limit resource utilization is surprising. 

> “Many companies adopt cloud for operational efficiency, but more than half of containers deployed have no limits, which could waste resources”
> **Sysdig**

![Sysdig report container resource limit image](resourcelimits.png)

Limits can be implemented either reactively where the system intervenes once it sees a violation or by enforcement, the system prevents the container from ever exceeding the limit by terminating it. Different runtimes can have different ways to implement the same restrictions, in the following sections we will set limits using different methods for Kuberentes, Fargate and Docker. 


## Setting resource limits in Kubernetes

When you configure resource limits in Kubernetes and a process in the container tries to consume more than the allowed amount of memory, the system kernel terminates the process with an out of memory (OOM) error. The CPU limit defineshow much CPU time the container can use, during each scheduling interval the kernel checks to see if this limit is exceeded and waits before allowing the process to resume execution. The Kubernetes API allows you to limit cpu, memory, ephemeral storage and hugepages.

In the following example there is a Pod named **cloudguardian** that defines a container named **codescan**, the limit of 1 CPU and 256MiB of memory and a request of 0.5 CPU and 128Mib of memory. The request property defines the minimum ammount of resources the container must have in order to be triggered, this way the scheduler ensures the node where the container will be allocated has sufficient resourcers to run it, on the other hand limits will set the boundary of resource consumption by the container.


```
---
apiVersion: v1
kind: Pod
metadata:
  name: cloudguardian
spec:
  containers:
  - name: codescan
    image: nginx
    resources:
      requests:
        memory: "64Mi"
        cpu: "250m"
      limits:
        memory: "128Mi"
        cpu: "500m"
```

## Implementing limits to your Containers and Pods in Fargate

## Setting Memory And CPU Limits In Docker
