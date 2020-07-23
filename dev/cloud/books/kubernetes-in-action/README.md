# Kubernetes in Action

## TOC

1. [Overview](#ch1and2): Viewing the entire datacenter as a single computational resource.
1. [Overview](#ch1and2)
1. [Pods](#ch3): A scalable, manageable group of containers that share a Linux namespace.
1. [Replication](#ch4): Use resource types to define replication controllers, that manage pods through health checks, failures, and scaling.
1. [Services](#ch5): Services sit in front of groups of pods and serve as a port of call for clients. Load balancers, DNS etc -- these are all services.

## Misc

[Kubectl Cheatsheet][kubectl-cheatsheet]

* `-o jsonpath='{.foo[*].bar....}'` can be used to select specific fields from the config/manifest
* `-o json` or `-o yaml` can be used to output the config|manifest

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

## Chapter 4: Replication<a name="ch4"></a>

[Detailed Notes][ch4-notes]

### Replication Q&A

* Container health
    * How are health checks conducted?
        * The Kubelet is entirely responsible for container health checks;
        * probes (**HTTP; TCP Socket; binary Exec**) are sent to each container at regular intervals -- **HTTP response codes, socket timeouts, exit codes**, these all express health;
        * repeatedly, the **Kubelet** will repeat health checks before taking action;
    * How does Kubernetes react to unhealthy pods?
        * The Kubelet **restarts the container**, the master node is not responsible in any way;
* ReplicationController
    * What is it?
        * It's a controller that's [part of the ControllerManager][controller-manager] in the master node;
    * What is it's purpose?
        * It's responsible for keeping an exact number of replica pods constant -- bringing up or destroying pods in the process;
    * How do they work?
        * The API server allows clients to observe resources. When a pod is destroyed, the (observing) controller is notified. The controller then measures the number of pods, and acts accordingly;
        * they target pods with a **specified label**, and monitor them;
    * How are they created?
        * A pod manifest allows the specification of a *kind* property, which is the kind of controller it essentially uses;
        * replication count, a template, and a name are also required;
    * When should they be used? 
* ReplicationSets
    * What are replication sets?
        * Almost identical to ReplicationContollers, except that they make use of more expressive selectors in the manifest; 
    * What is their purpose?
        * To replace RCs -- RSs should be used as a priority over RCs;
    * How do they work?
        * Exactly the same as RCs; 
    * When should they be used?
        * Whenever you intend to use an RC; 
    * How do they differ from replication controllers?
        * The make use of more expressive selector declarations in the manifest;
* DaemonSets
    * What are DaemonSets?
        * A pod, or a group of pods, that are run on each node, or a subset of nodes; 
    * What is their purpose?
        * To run some system level process on each selected node;
    * How do they work?
        * The DaemonSet controller works just like an RC, except there are no replicas at the node level, just across the cluster -- once per node; 
    * When should they be used?
        * Any time you have a task that requires exactly one set of pods per node is the domain for a DS;
* Periodic jobs
    * How are periodic jobs run?
        * By specifying a **CronJob** resource;
    * Why would you want to do this?
        * You may want to run a Job at set intervals;
* Scheduling a pod to run a single job then stopping
    * How is it achieved?
        * Through a **Job** resource
    * Why would you want to do this?
        * Not all tasks are suited to long-living resources, some only need to be done once -- perhaps in response to some event;

### Summary

**Manifests** are of a certain **kind**, in this example they are of the **ReplicationController kind**.  A ReplicationController is part of the **ControllerManager** in the **control plane**, and monitors pods to ensure that the exact number of **replicas** are kept running at all times -- essentially becoming fully responsible for the described pods. Pods come under the RC management when they have a **label** that matches the **selector** described in the **manifest**.

**ReplicaSets** are identical to ReplicationContollers, except that they make use of a more expressive selector declaration to pick pods that should be controlled by the RS.

**Jobs** are one-time tasks that run through to completion, perhaps in response to some event. They are useful in cases where the job *must* complete, because you can specify what to do in the event of job failure in the manifest. **CronJobs** are Job resources, except that they can be scheduled, and failed if the jobs fail to execute within a time frame. Because both make use of a Job resource, and job pods aren't destroyed when they complete, it's possible to pull logs from them.

Pod failures are determined through **health checks** which are simple **HTTP, TCP Socket, or Exec** probes, where the latter is a simple binary execution. Various methods are used to determine failure, like return codes, timeouts etc. These health checks are done at regular intervals, and repeated when failure is detected. It takes some amount of time for Kubernetes to determine and respond to the failure, which is by design.

## Chapter 5: Services<a name="ch5"></a>

[Detailed Notes][ch5-notes]

**Services** point to pods via **Endpoints** -- pod connection metadata. Endpoints are typically automatically created via Services, but you can specify them manually. Services are created whenever you **expose** some ports on a pod. To make your life easier, you should **specify a name for all mapped ports** -- that way the ports can be changed at a later date and it doesn't break anything. All services and ports are included into a pod's **environment variables** -- assuming the pod is spun up after service creation. All pods also resolve to an **internal DNS** server pod (see the container's resolv.conf), and all services can be reached via an **FQDN** -- which is the preferred method. DNS servers can be viewed with **`kubectl get po --namespace kube-system`** and a pod manifest **dnsPolicy** key can be used to control the DNS policy.

**NodePort, LoadBalancer, ExternalName**, and **Ingress** are all **_types_ of Services**, they are all declared as Services in a manifest, but their *type* is specified.

**ExternalName** is used to map one domain to another. It doesn't create a pod, but creates a **CNAME record** in the **DNS server** (pod). It's used to map internal pods to external services.

**NodePort** is a service (contains Endpoints), and it **opens a specified port on every node**, and maps them to **Endpoints**. Internal pods can make requests to this service via a ClusterIP, which is distributed evenly across nodes. NodePort does **SNAT**, so the recipient doesn't know the requester's IP, which can create problems, so **be warned**.

**LoadBalancer** is a generalisation of NodePort except that it offers a **publicly accessible IP**. To get it working you specify a selector for targeted pods, the public port to bind to, and the pod port to forward to. This works at the **IP level**, and each pod group needs its own LoadBalancer.

**Ingress** is also a load balancer, and a generalisation of NodePort. The difference between Ingress and LoadBalancer is that Ingress **works at the HTTP level** and on **request URLs** instead of IPs. This allows it to run as a **single instance**, and target multiple pod groups via their selectors. It does **TLS termination**, and should contain the **certificate and private key** -- which is stored in a **Secret** resource, and declared in the manifest. Automated certificate signing is possible through a **CertificateSigningRequest** resource. It's also possible that it can forward to **external services** via a domain name.

=> generalises | X-- composes

(**LoadBalancer|Ingress**) => **NodePort** => **Service** X-- **Endpoint** 

All services should have a **readiness probes** explicitly defined, otherwise application component will be declared ready instantly, when that isn't necessarily the case. These probes come in the form of **HTTP, TCP, or Exec probes**, and they will return some kind of code. Readiness probes should be used **to determine health** -- the application component's ability to accept and respond to connections -- in contrast to liveness probes, which just determine if a pod is alive. Readiness probes are declared in the controller manifest, and are periodically run, which is configurable. These probes can be run in such a way that allows for application components to do **internal health checks** -- which should probably do some mock test of integration points.


[ch1-2-mindmap]: ch1-2-intro/mindmap.png?raw=true
[ch1-2-notes]: ch1-2-intro/README.md
[ch3-mindmap]: ch3-pods/mindmap.png?raw=true
[ch3-notes]: ch3-pods/README.md
[ch4-notes]: ch4-replication/README.md
[ch5-notes]: ch5-services/README.md

[arch-overview]: ch1-2-intro/arch-overview.jpg?raw=true
[controller-manager]: https://kubernetes.io/docs/reference/command-line-tools-reference/kube-controller-manager/
[kubectl-cheatsheet]: https://kubernetes.io/docs/reference/kubectl/cheatsheet/
