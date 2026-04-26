// this file will be a draft for explaing part of chapter 5 (Encoding and Evolution) in 
Designing Data-Intensive Applications, 2nd Edition

// the part that I will start to explain is:
// Load balancers, service discovery, and service meshes
<!-- All services communicate over the network. For this reason, a client must know the address of the service it’s connecting to—a problem known as service discovery. The simplest approach is to configure a client to connect to the IP address and port where the service is running. This configuration will work, but if the server goes offline, is transferred to a new machine, or becomes overloaded, the client has to be manually reconfigured.

To provide higher availability and scalability, multiple instances of a service are usually running on numerous machines, any of which can handle an incoming request. Spreading requests across these instances is called load balancing [42]. Many load balancing and service discovery solutions are available:

Hardware load balancers
These specialized pieces of equipment are installed in datacenters. They allow clients to connect to a single host and port, and incoming connections are routed to one of the servers running the service. Such load balancers detect network failures when connecting to a downstream server and shift the traffic to other servers.

Software load balancers (such as NGINX and HAProxy)
These behave in much the same way as hardware load balancers, but rather than requiring a special appliance, they are applications that can be installed on a standard machine.

The Domain Name Service (DNS)
This is how domain names are resolved on the internet when you open a web page. It supports load balancing by allowing multiple IP addresses to be associated with a single domain name. Clients can then be configured to connect to a service via a domain name rather than an IP address, and the client’s network layer picks which IP address to use when making a connection. One drawback of this approach is that DNS is designed to propagate changes over longer periods of time and to cache DNS entries. If servers are started, stopped, or moved frequently, clients might see stale IP addresses that no longer have a server running on them.

Service discovery systems
These use a centralized registry such as etcd or Apache ZooKeeper rather than DNS to track which service endpoints are available (we’ll return to these systems in “Coordination Services”). When a new service instance starts up, it registers itself with the service discovery system by declaring the host and port it’s listening on, along with relevant metadata such as shard ownership information (see Chapter 7), datacenter location, and more. The service then periodically sends a heartbeat signal to the discovery system to signal that the service is still available.

When a client wishes to connect to a service, it first queries the discovery system to get a list of available endpoints, then connects directly to the endpoint. Compared to DNS, service discovery supports a much more dynamic environment where service instances change frequently. Discovery systems also give clients more metadata about the service they’re connecting to, which enables clients to make smarter load-balancing decisions.

Service meshes
This sophisticated form of load balancing combines software load balancers and service discovery. Unlike traditional software load balancers, which run on a separate machine, a service mesh load balancer is typically deployed as an in-process client library or as a process or “sidecar” container on both the client and server. Client applications connect to their own local service load balancer, which connects to the server’s load balancer. From there, the connection is routed to the local server process.

Though complicated, this topology offers advantages. Because the clients and servers are routed entirely through local connections, connection encryption can be handled entirely at the load balancer level. This shields clients and servers from having to deal with the complexities of SSL certificates and TLS. Mesh systems also provide sophisticated observability. They can track which services are calling each other in real time, detect failures, track traffic load, and more.

Which solution is appropriate depends on an organization’s needs. Those running in a very dynamic service environment with an orchestrator such as Kubernetes often choose to run a service mesh such as Istio or Linkerd. Specialized infrastructure such as databases or messaging systems might require their own purpose-built load balancers. Simpler deployments are best served with software load balancers. -->

// at first I want to include context of what chapter talked about
// starting from formats of encoding data (comparing json and binary formats)
// then moving to modes of data flow which talks about how data flow between services, databases and clients comparing how REST and RPC handle backword and forward compatability then reaching out to this paragraph that is under the Dataflow Through Services: REST and RPC part and talking about Load balancers, service discovery, and service meshes to say why it's included here and explain it in details

// so to do this we will give a breif about past topics to build context then dive deep on the Load balancers, service discovery, and service meshes part

// at first we want to clarify why we need load balancing: may be for deviding traffic between replicas, or in our case her having different versions of the same service, so using load balancer will route old clients to the old sercies and the new client to the new service

// for more clarificaiton I need to explain with visuals deployment stratigies that may be used with this type of services that mantain different versions

// then we will move to explain the load balancing technieques used here and how they solve our problem with the tradeoffs of every one. use diagrams when needed

I
// the output will be html that will be deployed using githup pages