# Cisco Data Center and Compute Management Platforms and APIs

## Cisco ACI
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





## Cisco UCS Manager
This section covers Cisco UCS Manager and the public APIs that come with it.

## Cisco UCS Director
This section goes over Cisco UCS Director and its APIs.

## Cisco Intersight
This section introduces Cisco Intersight and its REST API interface.
