# Kubernetes

## Components

#### Control Plane Components

The control plane's components make global decisions about the cluster \(for example, scheduling\), as well as detecting and responding to cluster events \(for example, starting up a new pod when a deployment's replicas field is unsatisfied\).

* `kube-apiserver`

  The API server is a component of the Kubernetes control plane that exposes the Kubernetes API. The API server is the front end for the Kubernetes control plane.

* `etcd`

  Consistent and highly-available key value store used as Kubernetes' backing store for all cluster data.

* `kube-scheduler`

  Control plane component that watches for newly created Pods with no assigned node, and selects a node for them to run on.

* `kube-controller-manager`

  Control Plane component that runs controller processes.

  1. Node controller: Responsible for noticing and responding when nodes go down.
  2. Replication controller: Responsible for maintaining the correct number of pods for every
  3. Endpoints controller: Populates the Endpoints object \(that is, joins Services & Pods\).
  4. Service Account & Token controllers: Create default accounts and API access tokens for new namespaces.

* `cloud-controller-manager`

  A Kubernetes control plane component that embeds cloud-specific control logic. The cloud controller manager lets you link your cluster into your cloud provider's API, and separates out the components that interact with that cloud platform from components that just interact with your cluster.

#### Node Components

* `kubelet`

  An agent that runs on each node in the cluster. It makes sure that containers are running in a Pod.

* `kube-proxy`

  kube-proxy is a network proxy that runs on each node in your cluster, implementing part of the Kubernetes Service concept.

## Pods

Pods are basically an abstraction to the container images. It is same as running a container.

![](https://theithollow.com/wp-content/uploads/2019/01/image-3.png)

## Replica Sets

Replica sets ensure that a specific number of replicas of a selected pod is running. It handles the high availability concern.

![Replica sets](https://theithollow.com/wp-content/uploads/2019/01/image-5-768x411.png)

## Deployments

Deployments ensure that we can safely rollout new version of our pods safely and without outages. It also support rollbacks.

![Deployment](https://theithollow.com/wp-content/uploads/2019/01/image-9-1024x375.png)

## Services

Each pod have a unique IP associated with them. Pods are created and destroyed without our intervention, so IP address of the pods will change. It will be really cumbersome to keep track of the IP's, that's were services come to help. Service is an abstract way to expose an application running on a sets of pods. The pods are selector with the selector.\(Each pod should have a label\)

### Cluster IP

Whenever we create a service a unique IP address is assigned to that service and this IP is called Cluster IP. Cluster IP remains same throughout it's lifetime. Cluster IP is an internal IP address, means it can only be assessed from within the cluster.

### NodePort

NodePort is responsible for redirecting external traffic to the Cluster IP. NodePort should be in range 30000-32767.

> [https://stackoverflow.com/questions/49981601/difference-between-targetport-and-port-in-kubernetes-service-definition](https://stackoverflow.com/questions/49981601/difference-between-targetport-and-port-in-kubernetes-service-definition)

### LoadBalancer

LoadBalancer is used to overcome the limitation of the NodePort. We can use an external load balancer from the cloud provider to listen at an arbitrary port\(like 443\) and redirect the traffic to the NodePort.

![](https://theithollow.com/wp-content/uploads/2019/01/image-20.png)

## Namespaces

Namespaces are used to logically separate a cluster. The three built-in namespaces are

1. Default - This is the namespace where all our pods and services  run unless we specify one
2. kube-public
3. Kube-System - This is namespace used by k8s internals.

## DNS

A DNS entry is created for every running service in the cluster. If Pod DNS is enabled, each pod will also get a dns entry.

![](https://theithollow.com/wp-content/uploads/2019/02/k8s-dns1-1.png)

## Ingress

Ingress in k8s object that routes the external traffic to the services. Unlike the LoadBalancer, ingress resource supports virtual hosting, URL routing and provide SSL. You need a Ingress controller like Nginx Ingress Controller to use Ingress resource.

## Secrets

Secrets are used to store sensitive configuration information. It can be either be stored as `data`\(must be base64 encoded\) or `stringData`\(unencoded\).

