# Setting Limits to your Linux Containers

You should be setting limits to your containers! I know the internet is full of quotes linking “setting limits” to uncreative attitude and bounderies to innovation, there is a known expression in my country; “Brazilians has no limits” to illustrate the curious and creative ways we use to solve problems in face of limitations, but we will see in this article that when it comes to Linux containers, it’s actually important to set resource limits.

By default there is no any mechanisms avoiding your containers to consume the all the memory available in your host, if a process is allowed to consume unlimited resources in your container, your cluster can quickly run out of Memory and CPU, disrupting your deployment thereby starving legitimate
applications. 

### In this article I will show you:

*	The reason why setting limits to your containers is important.
* How Cgroups limit resource usage in Linux. 
*	Implementing limits to your Containers and Pods in Fargate.
*	Setting Memory And CPU Limits In Docker.
*	Setting resource limits in Kubernetes. 





