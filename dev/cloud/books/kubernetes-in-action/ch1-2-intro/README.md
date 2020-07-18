# Kubernetes in Action: Part 1 - Overview

**Most of this part is skipped because it's common knowledge.**

## Notes

### 1.2.1: Understanding What Containers Are

Available namespaces:

* mount;
* process id;
* network: each interface belongs to one namespace;
* IPC;
* UTS: hostname/domain name;
* user id;

Cgroups can be used to limit not only CPU/RAM resources, but bandwidth too.

### 1.2.2: Introducing The Docker Container Platform

* images: contain layers, layers are parts of a realised system -- they are not slim build files;
* registry: push images to registry;
* containers are in fact dependent on the host kernel -- there can be incompatibilities;
* **Open Container Initiative**: an attempt to standardise container formats and runtime;
* **rkt**: another container engine with focus on **security**, **compostability**, and conforming to **open standards**;
* support: Kubernetes supports rkt;

### 1.3.2; Looking at Kubernetes from the Top of a Mountain

* Kubernetes can handle any size of cluster;
* it has a **master** and **worker** nodes;
* services offered: **service discovery, scaling, load-balancing, self-healing, leader election**;
* reduces focus on infrastructure: allows developers to focus on application code, not infrastructure;
* optimises resource utilisation: apps are automagically moved around between nodes for better resource utilisation;

### 1.3.3: Understanding the Architecture of a Kubernetes Cluster

* **master node**: the **control plane**, this manages the whole system;
* **worker node**: runs the deployed applications;

![Architecture Overview][arch-overview]

#### Control Plane

* **high availability**: the control plane can be split across multiple nodes for high availability;
* components
  * **API server**: you, and *other* (HA) control plane components communicate via this;
  * **scheduler**: assigns worker nodes to deployed components of your app;
  * **controller manager**: cluster level behaviours - replicating components, tracking worker nodes, handling failures etc;
  * **etcd**: a distributed store for cluster configuration;

#### Worker Nodes

These contain **multiple pods** and each pod contains **multiple containers**.

Node components:

* **container runtime**: Docker, rkt etc.;
* the **Kubelet**
    * interfaces with the control plane API server;
    * manages the node's containers;
* the **Kube proxy**: does load-balancing for application components[^1];

### 1.3.4: Running an Application in Kubernetes

#### Prepare an Application

1. package an application into one or more images;
1. push it to a registry;
1. post a *description* of the app in the API registry which contains:
    * an **image**, or application component[^1] **images**;
    * **relationships** between images;
    * which images are **co-located**[^2];
    * **exposed services** which will be discoverable;

#### Running an Application

1. the API server processes the description;
1. the scheduler schedules container groups to run on worker nodes, based on:
    * free resources;
    * computational requirements;
1. the worker nodes' Kubelet instructs the container runtime to pull the related image;

#### Understanding how the Description Works

An app description will describe multiple containers. The containers can be grouped (co-located[^2]) by assigning them to the same **pod**. Pods are scaled (called replicas[^3]). So essentially, descriptions contain pods, which contain containers.

#### Keeping the Containers Running

Kubernetes can be configured to run N number of containers where N is:

* an explicit number;
* determined by resource utilisation, such resources could be:
    * CPU;
    * memory;
    * queries per second;
    * any arbitrary metric you require;

#### Hitting a Moving Target

Kubernetes is capable of moving nodes around, and it will track any exposed services for you, which are then reached through a single IP. Requests to this IP are load-balanced (by Kube-proxy) between the relevant nodes. The IP can be reached through environment variables or DNS.

#### Understanding the Benefits of Kubernetes

Generally, applications can be deployed without consideration of the underlying server and hardware. But, if need be, you can configure Kubernetes to deploy certain containers to servers with specific hardware configurations -- like an SSD.

#### Achieve Better Utilisation of Hardware

* **considers resource requirements**: Kubernetes will consider, and deploy to, the servers that have the most suitable resource requirements;

#### Health Checking and Self-Healing

* **scaling the cluster**: Kubernetes can plug-into cloud APIs to scale the underlying infrastructure (in addition to managing the containers);

#### Simplifying Application Development

* **discovery**: is automagically managed -- no need to implement;
* the **API server**: provides a means for discovery, outside of DNS and environment variables[^4];
* **continuous delivery**: Kubernetes can detect misbehaving applications and stop the rollout;

[arch-overview]: arch-overview.jpg?raw=true

[^1]: **application components**: each application can be broken down into components, and distributed -- like microservices.
[^2]: **co-located containers**: sometimes different containers need to run on the same node to work.
[^3]: **replicas**: duplications of pods to be run in parallel;
[^4]: **environment variables**: can be used to map to exposed services;
