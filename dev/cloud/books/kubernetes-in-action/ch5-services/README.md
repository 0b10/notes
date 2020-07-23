# Kubernetes in Action: Services

## Prerequisite Knowledge

## Notes

### Services

* act as **load balancers** for the **pods** with the given **selector**;
* you can **create** a service through:
    * `kubectl expose`
    * manifest: `kubectl create -f service.yaml`
* aka [**Service**][service-docs] resource;
* **sessionAffinity** in the manifest spec allows you to send traffic to a specific pod, for every request;
* the ports section in the manifest can be used to expose **multiple ports**, but you **must specify a name**;
* ports can be given names. A pod manifest could specify ports, name them, and then you can use that name in the service manifest to target them -- e.g. **targetPort: https**
    * this allows you to change the port numbers in the pod spec later on, and make things **less brittle**;
* all services are exposed via container environment variables, where each container knows about all services -- the only caveat is that the pods must be created after the service, otherwise the env variable would not have been created within the containers;
    * \<service name\>_SERVICE_HOST=10.10.10.10
    * \<service name\>_SERVICE_PORT=80
* **dns**
    * there is a **dns server** running in the **kube-system namespace**: `kubectl get po --namespace kube-system`;
    * all containers have their **resolv.conf** modified to point to that
    * you can access other services via their **name** specified in their manifest -- e.g. my-service;
    * use the **dnsPolicy** in a pod's spec to control access to this
    * you can use a fully qualified domain name (**FQDN**) to access services
        * \<service name\>.\<namespace\>.\<cluster.domain.suffix\> -- see /etc/resolv.conf
        * service-name.default.svc.cluster.local
        * service-name.default.svc
        * service-name.default
        * service-name
* setting `ClusterIP: None` will cause a service to return all pod IPs when a DNS request is made

### Endpoints

* **Endpoint** is a resource, it and points to service endpoints -- pods
    * you can see endpoints with `kubectl get ep <optional service name>`;
    * you can manually create an Endpoints service with a manifest
        * must have the same name as the service
        * containers created after the EP will have the relevant environment variables
    * it's **created automatically** when you create a **service**
    * they can be used to point to **external endpoints**

### ExternalName

* is a type of **Service** resource
* can be used to **map an FQDN** to an **external service** -- containers use the FQDN to connect to external services
    * service-name.default.svc.cluster.local
        * can result in TLS cert error
* the external service is specified by a **domain name**
* the endpoints is **decoupled** from the service name -- the endpoint **can be changed** at any time
* this pod has **no IP** because it's simply a **CNAME record**[^1]

### NodePort

* is a service that opens up a port for each node, then forwards a connection to its own underlying service - which in turn is forwarded to pods;
* nodes appear to be chosen at random if you connect to the cluster ip
* is actually a **ClusterIP** service type;
* can be accessed via the service's **cluster IP** or directly via the **node's IP**;
    * the cluster IP sits in front of a group of node IPs; 
* manifest
    * **`nodePort: n`** is the only manifest property that should be used to define a NodePort
    * **`kind: Service`**
* generally found behind a **LoadBalancer**
* **SNAT** is performed in ingress traffic -- the source address is changed
* sometimes traffic is bounced to another node for whatever reason. This may be undesirable, use **`spec.externalTrafficPolicy: Local`** to prevent that
    * this can cause hanging if the pod doesn't exist on that node -- bad idea
    * with LoadBalancers, normally the connection is spread across all pods, but with this annotation traffic is only spread evenly across nodes -- each node may have a different number or replicas running on it, resulting in uneven distribution
    * there are some issues with **SNAT** which need to be considered [research]

### LoadBalancer

* is an extension of **NodePort**;
* it redirects all traffic to the specified node port, across all nodes;
* has its own **publicly accessible IP**
* manifest
    * **`kind: Service`**
    * **`type: LoadBalancer`**

### Ingress

* operates at the **HTTP level**;
    * request **URLs are parsed**, and so domain/foo can be routed differently than domain/bar
* Only a **single LB per cluster** is required. Normal LoadBalancers operate on IPs and require multiple of instances, but Ingress resources operate on URLs
* this looks like a good way to draw boundaries around parts of your application for microservices -- for example, /login having its own service
* can also be used to map to different **hosts / domains**, and not just different paths on the same host
* it does **TLS termination**
    * the **private key** and **certificate** are stored in a **Secret** resource, which is then referenced by name in the manifest via the **`spec.tls.hosts[*].secretName`** key
    * cert signing can be automated via the **CertifcateSigningRequest**

### Readiness Probes

* defined in the **controller** manifest under the **readinessProbe** key
* very similar to liveness probes
    * liveness checks for presence 
* when to use one?
    * **Health checks** -- e.g. can it connect to the backend database?
    * Can/wants to receive connections
* **TCP, HTTP, Exec**
    * for HTTP a special **URL** can be used to kick off an **internal check**
* returns some kind of **error code**
* done **periodically**
    * **configurable**
* if it's not ready the pod is removed from the service's Endpoints[^2], but not killed
* readiness is displayed in the **READY column** in pod info: `kubectl get po`
* **always define one**
* **caveats**
    * not including a probe means they become ready immediately, whether that's true or not 

## Sources

[service-docs]: https://kubernetes.io/docs/concepts/services-networking/service/

[^1]: CNAME record: a DNS record that points to an FQDN instead of an IP;
[^2]: Endpoint: a Kubernetes resource;
