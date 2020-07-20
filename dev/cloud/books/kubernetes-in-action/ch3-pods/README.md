# Kubernetes in Action: Pods

## Prerequisite Knowledge

* containers live inside pods;
* containers are co-located through pods;
* pods are assigned to worker nodes through the master node's scheduler;
* application components are parts of a larger application that are/should be containerised;

## Notes

### Justification

* they are *the* **deployable unit** -- containers are not;
* a pod is the basic **unit for scaling**;
* **co-located containers**:
    * all containers inside of pods are run on the same worker node;
    * processes sometimes require some form of coupling, they are sometimes related;
* pods are essentially **logical hosts** -- they have a single IP and their containers share a Linux namespace;
* **auto-management**: using pods allows Kubernetes to manage application components instead of the developer (inside of containers).

### Isolation

#### Containers

* containers in pods share the same set of Linux namespaces;
    * **UTS**[^1];
    * **Network**: they share the same interface, port space, and loopback;
    * **IPC**: they can do IPC
    * **PID**: ps shows processes from all containers;
* the **filesystem** is not shared between containers
    * you can use **volumes** to share files; 

#### Pods

* **isolated**: pods are isolated and do not share Linux namespaces
* **IP communication**: pods can communicate via IP
    * there is **no NAT** between pods
    * each pod has it's own, **single IP** 

### Management

#### Organising Containers Across Pods

* Why?
    * **Scaling**: different application components have different scaling requirements -- some are stateless, some are not;
    * **resource utilisation**: different pods means Kubernetes can schedule them differently;
* When?
    * **Frequently**: avoid pod sharing as much as you can;
    * **low coupling**: means using separate pods;
        * examples of high coupling:
            * sidecar[^2] containers;
            * containers that cannot be run on different hosts; are representative of a single whole;
    * **scaled independently**: if they do not need to be scaled together;

#### Creating

##### Manifest (YAML; JSON)

* you can post the manifest to the **REST endpoint**;
* primary manifest sections
    * **metadata**: name, namespace, labels etc.;
    * **spec**: pod contents -- image (list);
        * ports are always open -- they are for reference only;
* **help**: `kubectl explain pods` or `kubectl explain pods.spec`;

##### With Kubectl

* A limited method for creating pods; 
* **`kubectl create -f foo.yaml`** -- creates *any* resource from a yaml file;

### Logs

* you should **log to stdout/stderr**;
* docker logs stdout/stderr to files;
* **`kubectl logs <pod name>`**:
    * use -c for specific containers;
* logs are automatically **rotated**:
    * every 24hrs or 10MB;
    * only the last rotation is shown;
* use centralised logs if you want log persistence;

### Direct Connection

* you may want to **debug** a pod, so you may need a direct connection;
* use **port forwarding** from the localhost to a pod:
    * **`kubectl port-forward localhost:<src port> <dst port>`**

### Labels

* labels are used to **target groups** of pods -- which may consist of many **replicas** in a busy system;
* example of a good labelling system:
    * **app**: the app, component, or microservice the pod belongs to;
    * **release**: the release state -- stable; beta; canary release etc.;
* **add** labels to **existing pods**: `kubectl label po <pod> label_name=foo`  
* **change** labels: `kubectl label po <pod> label_name=foo --overwrite`
* **label selectors** can be used to select pods based on:
    * key: `label_name`;
    * negated key: `!label_name`;
    * key and value: `label_name=value`;
    * key and negated value: `label_name!=value`;
    * list: `label_name in (value1, value2)`
    * negated lists: `label_name not in (value1, value2)`
    * multiple selectors: `label1=value1,label2=value2`
* labels can be attached to **any object** -- pods, nodes etc; 
    * node: `kubectl label node <node_name> label_name=foo`;
* you can **schedule** pods to run in specific nodes with **nodeSelector** in the manifest, with a:
    * label: to target a group of nodes;
    * host name: to target a specific node -- but it could be unavailable;

### Annotations

* annotations add **descriptive fields**;
* they cannot be used as selectors;
* **avoid collisions**: `foo.com/myannotation`;
* `kubectl annotate pod <pod name> foo.com/myannotation="foo bar"`;
* can be added to existing nodes, or at creation time;

### Namespaces

* **draw boundaries** around groups of pods
    * creates **distinct groups**;
    * prevent **object name collisions**;
* you can use them to split environment into production, development etc;
* they don't provide isolation;
* from the [docs][kub-docs-namespaces]:
    * can be thought of as **virtual clusters**;
    * their purpose is to manage name collisions in environments with more than ~10 users;
    * **don't use them** unless they are needed;
* you can delete all pods in a namespace;

## Sources

[Namespaces | Kubernetes Docs][kub-docs-namespaces]

[kub-docs-namespaces]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/

[^1]: UTS: hostname/domain namespace;
[^2]: [sidecar pattern](https://dzone.com/articles/sidecar-design-pattern-in-your-microservices-ecosy-1): application components that share some common resource (coupled), and work to achieve similar/related goals; 
