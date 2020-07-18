# Kubernetes in Action

## Chapter 2 and 3: Introuction

### Summary

[Mindmap][ch1-2-mindmap]

Kubernetes allows developers to view an entire data centre as a single computational resource. It deploys application containers, does self-healing, service discovery, and load-balancing between containers.

Applications can be deployed with images, and a description. The description informs Kubernetes of the relationships between containers, and service exposure.

Kubernetes is designed to just work, in the most resource optimised way, to recover from failures, and scale.

The architecture consists of master and worker nodes. The master node controls how and when worker nodes and resources are allocated, and run. The worker nodes contain pods, which in turn contain containers. Master nodes and worker nodes contain other components that facilitate management and communication. All of this facilitates development by providing a platform that eases infrastructure management -- not just scaling, distribution, but also communication between application components.

### Kubernetes

* exposes the entire datacenter as a single computational resource;
* is constantly moving nodes around -- optimising resource utilisation; self-healing etc.;
* can plug into cloud APIs to scale the underlying infrastructure;
* helps continuous delivery by preventing bad rollouts (misbehaving nodes);
* can be configured to scale on any arbitrary metric;

![Architecture overview][arch-overview]

### Master Nodes (Control Plane)

* the **scheduler**
  * assigns applications to worker nodes;
  * optimises for resource utilisation;
* the **API server**
    * acts as an **interface** for clients, and worker nodes;
    * provides **service discovery** for exposed services
        * exposed as a single IP via the worker node's Kube Proxy;
* cluster configuration is stored in **etcd**, which is distributed;
* the **controller manager**
    * does a lot of the heavy lifting managing woker nodes;
* supports **high availability** -- multiple nodes;

### Worker Nodes

* contains a **Kubelet**, **Kube Proxy**, and a **container runtime**; 
* **pods**
    * nodes contain pods, which contain containers;
    * achieves co-location of containers by grouping them as a pod;
* **Kubelet**
    * manages containers;
        * instructs container runtime to pull image;
    * interfaces with the master node API server;
* **exposed services**
    * multiple nodes are exposed as a single IP;
    * can be reached via **environment variables, DNS**, or the master node **API server**;
    * the **Kube Proxy** does load balancing between nodes;

### Deploying and Running

Deployment involves packaging an application into **images**, pushing it to a **registry**, and providing a **description**. Descriptions contain **relationships, co-location** requirements, and **exposed services**.

Running an application involves: the API server **processing a description**, the scheduler **scheduling worker nodes**, and the worker node's Kubelet instructing containers to **pull the appropriate image**; 


[ch1-2-mindmap]: ch1-2-intro/mindmap.png?raw=true
[arch-overview]: ch1-2-intro/arch-overview.jpg?raw=true
