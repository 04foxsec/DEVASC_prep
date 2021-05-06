# Cisco Data Center and Compute Management Platforms and APIs

## Cisco ACI
The Cisco Nexus 9000 witches can run in two separate modes of operatio, depending on the software. The first mode is called standalone (or NX-OS) mode, which means the switches act like regular Layer 2/Layer 3 data center devices that are usually managed individually. In the second mode, ACI mode, the Cisco Nexus devices are part of an ACI fabric and are managed in a centralized fashion. 

Cisco Application Centric Infrastructure (ACI) is the SDN-based solution from Cisco for data center deployment, management, and monitoring. The solution is based on two components: the Cisco Nexus family of switches and Cisco Application Policy Infrastructure Controller (APIC).

Some of the features and capabilities of the Cisco APIC are as follows:
- Application-centric network policy for physical, virtual, and cloud infrastructure
- Data modelbased declarative provisioning
- Designed around open standards and open APIs
- Cisco ACI fabric inventory and configuration
- Software image management
- Fault, event, and performance monitoring and management
- Integration with third-party management systems such as VMware, Microsoft, and OpenStack
- Cloud APIC appliance for Cisco cloud ACI deployments in public cloud environments

The configuration of the ACI fabric is stored in the APIC using an object-oriented schema. This configuration represents the logical model of the fabric. The APIC compiles the logical model and renders the policies into a concrete model that runs in the physical infrastructure. 

Each of the switches contains a complete copy of the concrete model. When a policy that represents a configuration is created in the APIC, the controller updates the logical model. It then performs the intermediate step of creating a complete policy that it pushes into all the switches, where the concrete model is updated. The Cisco Nexus 9000 switches can only execute the concrete model when running in ACI mode. Each switch has a copy of the concrete model. If by any chance, all the APIC controllers in a cluster go offline, the fabric keeps functioning, but modifications to the fabric policies are not possible.

The Cisco ACI fabric is composed of physical and logical components. These components are recorded in the Management Information Model (MIM) and can be represented in a hierarchical management information tree (MIT). Each node in the MIT represents a managed object (MO). An MO can represent a concrete object, such as a switch, an adapter, a power supply, or a logical object, such as an application profile, an endpoint group, or an error message. All the components of the ACI fabric can be represented as managed objects.

The MIT hierarchical structure starts at the top with the root object and contains parent and child nodes. Each node in the tree is an MO, and each object in the fabric has a distinguished name (DN). The DN describes the object and specifies its location in the tree. The following managed objects contain the policies that control the operation of the fabric:

- APICs: These are the clustered fabric controllers that provide management, application, and policy deployment for the fabric.
- Tenants: Tenants represent containers for policies that are grouped for a specific access domain. 
  - User: User tenants are needed by the fabric administrator to cater to the needs of the fabric users.
  - Common: The common tenant is provided by the system. This tenant contains policies and resources that can be shared by all tenants.
  - Infra: The infra tenant is provided by the system and. It contains policies that manage the operation of infrastructure resources.
- Management: The management tenant is provided by the system. This tenant contains policies and resources used for in-band and out-of-band configuration of fabric nodes.
- Access policies: These policies control the operation of leaf switch access ports, which provide fabric connectivity to resources 
- Fabric policies: These policies control the operation of the switch fabric ports. Configurations for time synchronization, routing protocols, and DNS
- VM domains: Virtual machine (VM) domains group virtual machine controllers that require similar networking policy configurations. The APIC communicates with the VM controller to push network configurations all the way to the VM level.
- Integration automation framework: The Layer 4 to Layer 7 service integration automation framework enables a system to respond to services
- AAA policies: Access, authentication, and accounting (AAA) policies control user privileges, roles, and security domains for the ACI fabric.

### APIC policy building blocks
- Tenants are top-level MOs that identify and separate administrative control, application policies, and failure domains. A tenant can represent a customer in a managed service provider environment or an organization in an enterprise environment.
- VRFs are isolated routing tables. A VRF instance defines a Layer 3 address domain. A tenant can contain one or multiple VRF instances. VRF instances exist on any leaf switch that has a host assigned to the VRF instance. All the endpoints within a Layer 3 domain must have unique IP addresses because traffic can flow between these devices if allowed by the policy.
- Bridge domains represent the Layer 2 forwarding domains within the fabric and define the unique MAC address space and flooding domain for broadcast, unknown unicast, and multicast frames. Each bridge domain is associated with only one VRF instance, but a VRF instance can be associated with multiple bridge domains. Bridge domains can contain multiple subnets, which is different from regular VLANs, which are usually associated with only one subnet each.
- Subnets are the Layer 3 networks that provide IP address space and gateway services for endpoints to be able to connect to the network. Each subnet is associated with only one bridge domain. Subnets can be the following: Public (advertised), Private (az), Shared (route leaked)
- External bridged networks connect the ACI fabric to legacy Layer 2/Spanning Tree Protocol networks. This is usually needed as part of the migration process from a traditional network infrastructure to an ACI network.
- External routed networks create a Layer 3 connection with a network outside the ACI fabric. Layer 3 external routed networks can be configured using static routes or routing protocols such as BGP, OSPF, and EIGRP
- Application profile defines the policies, services, and relationships between EPGs. An application profile contains one or more EPGs. The application profile contains as many EPGs as necessary, and these EPGs are logically related to providing the capabilities of the application.
- The EPG is the most important object in the policy model. An EPG is a collection of endpoints that have common policy requirements, such as security, virtual machine mobility, QoS, or Layer 4 to Layer 7 services. In the Cisco ACI fabric, each endpoint has an identity represented by its address, a location, and attributes, and it can be physical or virtual. Each EPG can only be related to one bridge domain.
- Contracts define the policies and services that get applied to EPGs. 
  - Contracts can be used for redirecting service to a Layer 4 to Layer 7 device, assigning QoS values, and controlling the traffic flow between EPGs. EPGs can only communicate with other EPGs based on contract rules. 
  - Contracts specify the protocols and ports allowed between EPGs. If there is no contract, inter-EPG communication is disabled by default. 
  - For intra-EPG communication, no contract is required as this traffic is always allowed by default. 
  - The relationship between an EPG and a contract can be either a consumer or a provider. 
  - EPG providers expose contracts with which a consumer EPG must comply. 
  - When an EPG consumes a contract, the endpoints in the consuming EPG can initiate communication with any endpoint from the provider EPG.

### APIC REST API
The APIC REST API is a programmatic interface that uses the REST architecture. The API accepts and returns HTTP or HTTPS messages that contain JSON or XML documents. Whenever information is retrieved and displayed, it is read through the REST API, and whenever configuration changes are made, they are written through the REST API. The REST API also provides a way of subscribing to push-based event notification, so that when a change occurs in the MIT, an event can be sent through a web socket.

The generic APIC REST API URI looks as follows:
```
https://APIC_Host:port/api/{mo|class}/{dn|classname}.{xml|json}?[options]
```















## Cisco UCS Manager
This section covers Cisco UCS Manager and the public APIs that come with it.

## Cisco UCS Director
This section goes over Cisco UCS Director and its APIs.

## Cisco Intersight
This section introduces Cisco Intersight and its REST API interface.
