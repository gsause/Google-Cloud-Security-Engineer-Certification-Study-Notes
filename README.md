# Google-Cloud-Security-Engineer-Certification-Study-Notes

design and implement secure workloads and infrastructure on Google Cloud.

Google cloud offering - Storage, Compute, Big data, Machine Learning, Application services for web, mobile, analytics, and back-end solutions.

Cloud computing is a way of using IT that has these important traits
- customer gets computing resources over internet, self-service with scalable resource and pay only for what they use.

Resource, project, folder, organization node heirarchy.

custom roles cant be applied to folder level.

vpc peering (connect two VPC networks), shared vpc XPN (share VPC subnets across other projects).
udp traffic load balancing - Regional External Passthrough Network load balancer.

cloud identity manage users like AD

edge caching using cloud cdn

cloud storage - blob storage >10MB (5TB per obj)

Storage - standard(hot), nearline(30), cold(90), archive(365)

Storage Transfer service (schedule batch transfer from other providers, PB) or transfer appliance (rachable, lease fron G, load PB, send to GC DC)
 
Cloud SQL (Full SQL, online transactions, exsisting applications, upto 64 TB)

 spanner (SQL relational database management, 100k io per sec)

Firestore (Nosql, retreive bot individual and all docs, cache data even if data offline.)

Bigtable (low latency high throughput, >1TB, rapid natural semantic data, ML data)

VPC by default on auto mode has one subnet in each region.

nic's cant be modified after vm creation.

gcp network service, premium tier through googles network, standard through isp network.

vpc a to b only through external ip, unless, vpc peering or vpn for internal ip com.

Cloud Interconnect establishes direct, private connections between your on-premises network and your VPC network.

Cloud DNS route on weighted round robin, geoloc, privatezones.

If a firewall rule deny & allow has same priority, deny will be overrided. 

Cloud IDS creates a peered network of mirrored VMS's (packet mirroring), use that traffic and palo alto threat protection techs

best.prac 
-zero trust net model
-sec con oprem to GC
-disable default network
-automate infra provisioning
-use waf
-monitor net

Cloud Functions makes connecting your platform simple to build and easy to maintain, you are just responsible for the code.

Dedicated Interconnect- to connect to colocation facility, Letter of Authorization and Connecting Facility Assignment, creates vlan bgp con. 2-100Gbps con or 8-10Gbps con

If unreacheable geo loc. requires high bandwidth, low latency connectivity, use partner con with SP network. 

transfer data btwn azure and gcp use cross cloud interconnect

Low volume, no fibernet for interconnect, - cloud vpn

Low bandwidth, high availability, sec con- HAP-VPN

titan chip, crytographic signatures for privacy and remote procedure call for integrity to communicate each other.

google API requests are done via a REST service call.

VPC peering, which enables the resources in your VPCs to communicate across private RFC1918 space, which reduces exposure to attack.

mechanisms to control access: firewall rules, shared vpc, vpc service controls, vpc peering, cloud vpn.

cloud armour has preconfigured waf rules.

customer supplied keys, customer managed keys, external key manager?

Using Access Approval together with Access Transparency, means explicit consent is needed before Google support or Google engineers can access your project’s data.

Note that a key difference between GCDS and Managed Microsoft AD is that GCDS syncs to Google from on-premises AD, while Managed Microsoft AD is a hardened Google Cloud service running actual Microsoft AD.

Google Cloud Directory Sync is to replace exsisting AD/LDAP

Org, Floders, Projects, Resources, Member and roles, This Google Cloud resource hierarchy allows you to map your organization onto appropriate Google Cloud objects 

A policy is a collection of access statements attached to a resource.
irl, policy is a guidline to guide decision making to achive a rational outcome.

list and boolean constraints 
 
policy troubleshooter must be granted security reviewer role.

principals- users, service accounts, groups, and domains

a less restrictive parent policy will always override a more restrictive resource policy, for a project editor, you cannot restrict their access to a specific resource within that project however you can create deny policies to prevent access. 

Best to assing roles to groups than individuals.

Service Accounts control server-to-server interactions and are used to authenticate from one service to another.

 connection is considered active if at least one packet is sent every 10 minutes.

priority is the lowest possible (65535)

When applying firewall rules, you should consider using service account firewall rules instead of tag-based rulesThe reason for this is that tag-based firewall rules can be applied by any user who has the Compute Engine Instance Admin role, but users require explicit IAM rights to use a service account.

Shared VPC Admins can delegate network administration tasks to Network and Security Admins

Cloud VPN securely connects your peer network to your Virtual Private Cloud network through an IPsec VPN connection.

Cloud Interconnect extends your on-premises network to Google's network through a highly available, low latency connection.

VPC Service Controls: Adds a security perimeter around Google Cloud services to prevent unauthorized data access or exfiltration.

Private Google Access: Allows VPC resources without public IPs to securely access Google APIs and services over Google's internal network.

Access Approval: Requires explicit approval before Google Cloud personnel can access sensitive resources, ensuring oversight and control.

Service accounts are an identity that a resource such as a VM instance can use to run API requests on your behalf.

The Trusted Images Policy can be used to enforce which images can be used in your organization.

Sheilded vm- intergrity, no kernel boot compromise  , conf vm- encrypted, isolated

In general, Google recommends that each instance that needs to call a Google API should run as a service account with the minimum permissions necessary for that instance to do its job.

You can also use OS Login to manage SSH access to your instances using IAM without having to create and manage individual SSH keys.

keyzar in kek

Customer-supplied encryption keys CSEK - customer bring their own key
Customer-managed encryption keys CMSK - google takes cares of key management and rotation
Cloud EKM Cloud External Key Manager- uses key that customer manages using external key management partner.
 
Objects get another layer of encryption on top of Google’s automatic encryption using keys you manage in Google's Cloud Key Management Service.

Hardware Security Module supports FIPS 140-2 is a US government computer security standard for cryptographic modules. An attestation statement shows that the key is HSM-protected. the attestation is essentially a signed statement that's verified by both Google and the HSM.

Kubernetes is a virtualized environment in which you run, manage, and scale applications. Each application runs in a container. A container is a lightweight, isolated user space for running application code. they contain a very scaled-down operating system with just the bare minimum needed to run a container. 

Starting and stopping a container means starting and stopping its scaled down operating system processes, not booting an entire vm and initializing an operating system. Similar to a vm, a container has its own filesystem, CPU, memory, process space, and more. Because they are decoupled from the underlying infrastructure, they are portable across clouds and OS distributions.

Containers execute within a pod. This is useful when containers are tightly coupled or share resources.

Nodes are the worker machines on which the pods exist. ech node is seperate vm with its own OS. Nodes provide services to the pods, such as hardware and the network infrastructure.

Clusters are a set of one or more nodes. The control plane, which is the primary node, controls the other nodes in the cluster. GKE manges that control plane.

best practice - upgrade, if auto-upgrade disabled, schedule it. health checks twice a day. 
Artifact Registry, which ensures only approved container images can be deployed.

app performance management tools - Trace - latency data, profiles - heat map of resource use.

Monitoring - The process of collecting, analyzing, and using information to track applications and infrastructure in order to guide business decisions.

Cloud Monitoring provides visibility into the performance, uptime, and overall health of cloud-powered applications. metric, events, metadata and provides dashboard insights.

Cloud Logging allows users to collect, store, search, analyze, monitor, and alert on log entries and events. log explorer, analytics and error reporting.

When you create a Google Cloud project, that project hosts a metrics scope and becomes the scoping project for that scope. It stores the alerts, uptime checks, dashboards, and monitoring groups that you configure for the scope. You can add multiple projects to an existing scope.

Uptime checks can help us ensure that our externally facing services are running and availabe

project that hosts metrics scope is Scoping project.

Service level indicators - metric that ,easure one aspect of service relaibility. no of good events/count of valid events. (things that you measure)

Service level objective - combine SLI with target relaibility. 99.9% (represents achievable target)

Service Level Agreements are commitments made to your customers that your systems and applications will have only a certain amount of down time.

SLA describes the minimum levels of service that you promise to provide to your customers and what happens when you break that promise.  

profiler provides flame graphs  
