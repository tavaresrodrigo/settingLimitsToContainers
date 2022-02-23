# Setting Limits to your Linux Containers

You should be setting limits to your containers! I know the internet is full of quotes linking “setting limits” to uncreative attitude and bounderies to innovation, there is a known expression in my country; “Brazilians has no limits” to illustrate the curious and creative ways we use to solve problems in face of limitations, but we will see in this article that when it comes to Linux containers, it’s actually important to set resource limits.

By default there is no any mechanisms avoiding your containers to consume the all the memory available in your host, if a process is allowed to consume unlimited resources in your container, your cluster can quickly run out of Memory and CPU, disrupting your deployment thereby starving legitimate
applications. 

### In this article I will show you:

*	Setting limits to your containers is important.
* How Cgroups limit resource usage in Linux. 
*	Implementing limits to your Containers and Pods in Fargate.
*	Setting Memory And CPU Limits In Docker.
*	Setting resource limits in Kubernetes. 


### Setting limits to your containers is important

By setting resource limits to your containers, you protect your environment to from attacks like [resource exhaustion attack](https://en.wikipedia.org/wiki/Resource_exhaustion_attack), improve efficiency in resources utilization, promote a more efficient resource allocation, and minimize costs. 

By applying limits to resource utilization for your containers you also improves visibility on how much memory and CPU the conainer process is demanding from the host operation system. In the Sysdig 2022 Cloud‑Native Security and Usage Report Sysdig shared some interesting finds based on the data gattered from the billions of containers their customers run over the course of a year and the ammount of workloads that does not limit resource utilization is surprising. 

> “Many companies adopt cloud for operational efficiency, but more than half of containers deployed have no limits, which could waste resources”
- Sysdig

[Sysdig report container resource limit image](resourcelimits)

Limits can be implemented either reactively (the system intervenes once it sees a violation) or by enforcement (the system prevents the container from ever exceeding the limit). Different runtimes can have different ways to implement the same restrictions.




