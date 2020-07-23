# Kubernetes in Action: Replication

## Prerequisite Knowledge

* pods are automatically scheduled to run on nodes;
* nodes are virtual/physical servers (resources) that are part of a cluster;
* pods are run on nodes;
* pods contain containers;
* the Kubelet is a component that runs on the node and manages containers;
    * it interfaces with the master node's API server;

## Misc

* the apiVersion in the manifest has two parts: group/version
    * apiVersion: app/v1
    * apiVersion: core/v1
    * apiVersion: v1
        * same as core/v1


## Notes

### Misc

* you almost never create pods directly, you typically create other resources like **ReplicationContollers** or **Deployments**;
* manually creating pods means they are **unmanaged**. Although the containers in a pod will be managed, if the node goes down, it's lost -- a new node won't be spun up, and a pod won't automatically be run on it;

### Container Health

* Container health can be measured using a **liveness probe** -- a request in one of three ways:
    * an **HTTP GET request**: HTTP error codes or not response will cause failure;
    * a **TCP Socket probe**: a fully established connection is a pass;
    * an **Exec probe**: run an arbitrary binary within a container;
* The **Kubelet** is responsible for probing container health;
* Containers are **restarted** when a liveness probe fails
* **livenessProbe**: is part of the image spec in the manifest;
* one suggestions is to use a specific endpoint like /health, so that the app can run an internal health check, instead of just a basic HTTP/TCP Socket connection test;
    * keep this discrete, check internal health only, don't include any backend integrations -- like a database;
    * keep it light, heavy lifting isn't a good idea;
* Kubernetes will automatically retry the liveness probe n number of times -- no need for a custom loop; 

### ReplicationControllers


#### Notes

* **monitors pod health**: if a pod or it's node disappears, then it responds;
* only pods of a specified **label** are maintained at a specified quantity -- less or more causes a response;
    * **label selector**: the target pods;
    * **replica count**: the number of desired pods to maintain;
    * **pod template**: for creating new pods;
* caveats
    * if a pod is not monitored by a replication controller, it isn't replaced if it goes down;
    * the RC doesn't care about pod state;
    * **name collisions** can occur with **selectors**;
    * pods are destroyed and recreated if the assigned node changes -- they are not migrated;
* selectors and scope
    * removing/changing a label will **orphan** a pod, whether deliberate or not;
    * metadata.ownerReference in the pod manifest (`kubectl get pods --output=yaml`) describes the owning RC -- good to know in case of orphans;
    * pods must have all labels referenced by the selector;
* kubectl commands and `kubectl edit` essentially do the same thing, and both edit the RCs definition -- either way is suffice;

#### Create

The following must be included in the manifest to create an RC:

* **`kind: ReplicationController`**;
* give it a **name**;
* specify the **number of replicas**;
* specify **selector** for which the controller is responsible for;
* specify a **template** which describes the pod contents;

How does an RC relate to a pod/manifest?

* the manifest is of a certain **kind** -- e.g. a ReplicationController etc;
* the RC manifest describes the pods that it will create and manage;

```sh
# Create a ReplicationController via a manifest
kubectl apply -f some-manifest.yaml
```

```yaml
# An example of a ReplicationController manifest
apiVersion: v1
kind: ReplicationController
metadata:
  name: nginx
spec:
  replicas: 3
  selector:
    # avoid name collisions, otherwise the RC will automatically manage those labels
    app: nginx  # [optional] the RC is responsible for ALL pods with this selector
  template:  # used to define what the controlled pod looks like
    metadata:
      name: nginx  # the pod name, instances are suffixed: nginx-lcruj
      labels:
        app: nginx  # pod labels: can be used instead of the above selector
    spec:
       containers:  # pods are made up of a number of containers
       - name: nginx
         image: nginx  # the docker image to pull from the registry
         ports:
         - containerPort: 80
```

#### Cheatsheet

```sh
# INFO
kubectl get rc  # a list of RCs
kubectl describe rc <rc-name>  # more specific, detailed information
# SCALING
kubectl scale --replicas=5 rc/nginx  # rc == ReplicationController
# DELETE
kubectl delete rc -l name=nginx  # delete the RC, scale to zero
kubectl delete rc -f rc-manifest.json  # use the RC manifest instead
kubectl delete rc <rc name> --cascade=false  # keep the pods
# EDIT
kubectl edit rc <rc name> # changes sometimes don't occur until pods are reloaded
```

### ReplicationSets

[ReplicaSet | Docs][rs-docs]

* ReplicationSets vs ReplicationControllers
    * almost identical to ReplicationControllers;
    * **preferred** to RCs;
    * the only difference is a more powerful label selector system;
    * differences in the manifest
        * apiVersion: apps/v1
        * kind: ReplicaSet
        * plus a few other small changes
        * selectors
          * you can specify multiple matchLabel and matchExpression values; 
          * [**matchLabel**][match-docs]: match labels equivalent to - "label in [list]";
          * [**matchExpression**][match-docs]: similar to matchLabel except it's more expressive - can use "in", "exists", "notExists" etc;
              * exists: the pod must have the specified *key* -- the value doesn't matter;
              * noExists: the pod must not have the specified *key*
* you don't create them directly, but when you create a higher level **Deployment** resource;

### DaemonSets

[DaemonSet | Docs][ds-docs]

* run exactly **one pod per node**;
    * system-wide operations etc;
    * kube-proxy is a DaemonSet;
    * you can run systemd services instead, but you will miss out on Kubernetes features;
* you can use node selectors to run on a **subset** of nodes;
* pods managed by a DS **bypasses the scheduler**;
* uses the **nodeSelector** manifest prop under the template spec;
* supports **matchLabel** and **matchExpression** in the manifest for selectors
* the command **`kubectl get ds`** will show you all DSs


### Periodic Jobs

[CronJob | Docs][cj-docs]

* aka the **CronJob** resource;
* essentially a **Job** resource that's run at **specific times**;
* part of the batch **API** group: **batch/v1beta1**;
* you can set a deadline, a time window that the job must start within at the given time: **startingDeadlineSeconds** -- in other words there's a way to ensure that the job is started promptly. The job will show as failed, and not run if the deadline isn't met;
* jobs should be **idempotent** so that in the case where multiple jobs are run by mistake, the results are the same regardless;


### One-time Jobs

[Jobs | Docs][jobs-docs]

* **Job** resource;
* runs once, then the pod exits;
* on failure, it can be configured to restart, or just exit -- see the manifest property: **onFailure**;
* useful when you have a job that absolutely must complete;
* part of the batch **API** group: **batch/v1**;
* pods aren't deleted on completion, so that the **logs** can be examined;
    * you must delete the Job resource or the pod itself;
* jobs can contain **multiple pods** and can run in **parallel** or **sequentially**, see the **manifest props**:
    * **completions**: the number of times to run the same job sequentially;
    * **parallelism**: the number of parallel jobs;
* you can create a **timeout** with the manifest prop: **activeDeadlineSeconds**;

## Sources

* [DaemonSet | Docs][ds-docs]
* [Job | Docs][jobs-docs]
* [ReplicaSet | Docs][rs-docs]
* [ReplicationController | Docs][rc-docs]

[rc-docs]: https://kubernetes.io/docs/concepts/workloads/controllers/replicationcontroller/
[rs-docs]: https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/
[match-docs]: https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/#set-references-in-api-objects
[jobs-docs]: https://kubernetes.io/docs/concepts/workloads/controllers/job/
[ds-docs]: https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/
[cj-docs]: https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/
