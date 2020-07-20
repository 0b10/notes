# Kubernetes in Action

## TOC

1. [Overview](#ch1and2): Viewing the entire datacenter as a single computational resource.
1. [Overview](#ch1and2)
1. [Pods](#ch3): A scalable, manageable group of containers that share a Linux namespace.

## Chapter 1 and 2: Overview<a name="ch1and2"></a>

### Summary

* [Mindmap][ch1-2-mindmap]
* [Detailed Notes][ch1-2-notes]

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

## Chapter 3: Pods<a name="ch3"></a>

* [Mindmap][ch3-mindmap]
* [Detailed Notes][ch3-notes]

### Key Takeaways

* pods are isolated from each other via Linux namespaces;
* containers in the same pod share the same Linux namespaces -- only the file system is isolated;
* pods are the basic unit for scaling;
* pods are for highly coupled containers;
* avoid putting containers in the same pod where possible -- only do it where it makes sense;
* containers should log to stdout/stderr, `kubectl logs` can read pod logs them from disk;
* labels are used to conditionally select groups of pods;
* labels can apply to any Kubernetes object -- nodes, pods etc;
* use annotations for description purposes, but avoid naming collisions;
* namespaces can be used to prevent name collisions, or set up boundaries for different development environments like dev, production etc.
* namespaces are only to be used in systems with many users, and name collisions are a problem;

## Pods Q&A

* What are they?
    * A *mandatory* means to group containers so that they can share resources;
* Why are they needed?
    * To provide a shared Linux namespace for containers -- sometimes application components need easy access to other application components;
    * to provide a mechanism to scale containers together;
* What specific features do they offer?
    * Shared resources -- shared Linux namespace -- IPC, network, PID etc;
    * a single IP to interface with, regardless of replication;
* What features are related to them?
    * Pods are a fundamental object, and Kubernetes would cease to work without them -- so all features relate to them;
    * labels, namespace etc. are used to select them;
    * port forwarding can be used to directly connect to a pod for debugging purposes;
* How are they managed?
    * Kubernetes manages them, by scheduling them to run on appropriate nodes;
    * labels can be used to target groups of related pods;
    * the manifest can be used to create pods with specific properties;
    * nodeSelector in the manifest can be used to schedule pods to run on nodes with specific labels;
* How are they used?
    * To contain, run, and scale containers that are tightly coupled;
* How are they created?
    * Through the manifest, or via `kubectl create ...`;
* How are they destroyed?
    * `kubectl delete ...` or by deleting all pods contained in a namespace;
* How can they be activated?
    * By creating them -- sending a create command to the API server (via CLI or manifest); 
* How are they deactivated?
    * By deleting them -- sending a delete command to the API server (via CLI);

### Summary

Pods are the **basic unit of scaling**, and can be thought of a **virtual host** -- where each container could be a process. Containers in pods share the **same Linux namespace**, and can communicate via traditional IPC mechanisms, however, each container file system has its own namespace -- so files cannot be shared unless a Kubernetes volume is used. Inter pod communication is done through IP, which isn't separated by NAT.

You want to co-locate containers in pods if they have tight coupling (like sidecars), or if they should scale together -- try to avoid it though.

Pods are declared in a **manifest** file: the **spec** - which contains the pod contents, and **metadata** --  labels, annotations and namespaces etc. 

Containers should **log** to stdout/stderr, and sent to a centralised location if you require persistence.

**Labels** are necessary to target commands to replicated/groups of pods, nodes, or any Kubernetes object -- the nodeSelector in the manifest file can be used schedule pods to run on nodes with specific labels, for example. **Annotations** only provide descriptive information, and **namespaces** are used to alleviate name collisions in large complex organisations. 

[ch1-2-mindmap]: ch1-2-intro/mindmap.png?raw=true
[ch1-2-notes]: ch1-2-intro/README.md
[ch3-mindmap]: ch3-pods/mindmap.png?raw=true
[ch3-notes]: ch3-pods/README.md
[arch-overview]: ch1-2-intro/arch-overview.jpg?raw=true
