# What Is an SDK?:
An SDK (software development kit) or devkit is a set of software development tools that developers can use to create software or applications for a certain platform, operating system, computer system, or device. An SDK typically contains a set of libraries, APIs, documentation, tools, sample code, and processes that make it easier for developers to integrate, develop, and extend the platform. An SDK is created for a specific programming language, and it is very common to have the same functionality exposed through SDKs in different programming languages.

As you will see in this chapter and throughout this book, where there is an API, there is usually also an SDK. Software developers can, of course, implement and spend time on developing code to interact with an API (for example, building their own Python classes and methods to authenticate, get data from the API, or create new objects in the API), or they can take advantage of the SDK, which makes all these objects already available.

A good SDK has these qualities:
- Is easy to use
- Is well documented
- Has value-added functionality
- Integrates well with other SDKs
- Has minimal impact on hardware resources

SDKs provide the following advantages:
- Quicker integration
- Faster and more efficient development
- Brand control
- Increased security
- Metrics

# Cisco Meraki: 
From a programmability perspective, the Meraki cloud platform provides several APIs:

- Captive Portal API extends the power of the built-in Meraki splash page functionality by providing complete control of the content and authentication process that a user interacts with when connecting to a Meraki wireless network. Meraki network administrators can completely customize the portal.
- Scanning API akes advantage of Meraki smart devices equipped with wireless and BLE (Bluetooth Low Energy) functionality to provide location analytics and report on user behavior. This can be especially useful in retail, healthcare, and enterprise environments, where business intelligence and information can be extracted about trends and user engagement and behavior. The Scanning API delivers data in real time and can be used to detect Wi-Fi and BLE devices and clients.
- MV Sense Camera API akes advantage of the powerful onboard processor and a unique architecture to run machine learning workloads at the edge. Through the MV Sense API, object detection, classification, and tracking are exposed and become available for application integration.
- Dashboard API provides endpoints and resources for configuration, management, and monitoring automation of the Meraki cloud platform. 
  - Provisioning new organizations, administrators, networks, devices, and more
  - Configuring networks at scale
  - Onboarding and decommissioning of clients
  - Building custom dashboards and applications

Get access to the Dashboard API: Cisco Meraki dashboard at https://dashboard.meraki.com  Organization > Settings. From there, at the bottom Enable Access. Once you have enabled the API, select your username at the top-right corner of the web page and select My Profile. In your profile, scroll down and locate the section named Dashboard API Access and select Generate New API Key. The API key you generate is associated with your account. You can generate, revoke, and regenerate your API key in your profile. Make sure you copy and store your API key in a safe place.

Every Dashboard API request must specify an API key within the request header. If a missing or incorrect API key is specified, the API returns a 404 HTTP error message. 
The key for the authentication request header is **X-Cisco-Meraki-API-Key**, and the value is the API key you obtained previously. In order to mitigate abuse and denial-of-service attacks, the Cisco Meraki Dashboard API is limited to 5 API calls per second per organization. In the first second, a burst of an additional 5 calls is allowed, for a maximum of 15 API calls in the first 2 seconds per organization. If the rate limit has been exceeded, an error message with HTTP status code 429 is returned. The rate-limiting technique that the Dashboard API implements is based on the token bucket model. 

The Cisco Meraki Dashboard API uses the base URL **https://api.meraki.com/api/v0** (or some redirected domain). Keep in mind that the API will evolve, and different versions will likely be available in the future. Always check the API documentation for the latest information on all Cisco APIs, including the Meraki APIs, at https://developer.cisco.com.

For accessing the API you need an **API key** and  **curl, Postman, Python's request module or something else that can talk to an API**
API call to get the organizations:

```curl -I -X GET --url 'https://n149.meraki.com/api/v0/organizations' -H 'X-Cisco-Meraki-API-Key: 15da0c6ffff295f16267f88f98694cf29a86ed87' -H 'Accept: application/json'
...
[
   {
   "name" : "DevNet Sandbox",
   "id" : "549236"
   }
]
```
Getting the netwroks under the Devnet Sandbox:

```curl -X GET --url 'https://n149.meraki.com/api/v0/organizations/549236/networks' -H 'X-Cisco-Meraki-API-Key: 15da0c6ffff295f16267f88f98694cf29a86ed87' -H 'Accept: application/json'
...
[
  {
  "timeZone" : "America/Los_Angeles",
  "tags" : " Sandbox ",
  "organizationId" : "549236",
  "name" : "DevNet Always On Read Only",
  "type" : "combined",
  "disableMyMerakiCom" : false,
  "disableRemoteStatusPage" : true,
  "id" : "L_646829496481099586"
  },
  {
  "organizationId" : "549236",
  "tags" : null,
  "timeZone" : "America/Los_Angeles",
  "id" : "N_646829496481152899",
  "disableRemoteStatusPage" : true,
  "name" : "test - mx65",
  "disableMyMerakiCom" : false,
  "type" : "appliance"
}, ... omitted output
```
Obtain a list of all devices that are part of the network that has the name 'DevNet Always On Read Only' and ID L_646829496481099586
```curl -X GET --url 'https://n149.meraki.com/api/v0/networks/L_646829496481099586/devices' -H 'X-Cisco-Meraki-API-Key: 15da0c6ffff295f16267f88f98694cf29a86ed87' -H 'Accept: application/json'
...
[
  {
  "wan2Ip" : null,
  "networkId" : "L_646829496481099586",
  "lanIp" : "10.10.10.106",
  "serial" : "QYYY-WWWW-ZZZZ",
  "tags" : " recently-added ",
  "lat" : 37.7703718,
  "lng" : -122.3871248,
  "model" : "MX65",
  "mac" : "e0:55:3d:17:d4:23",
  "wan1Ip" : "10.10.10.106",
  "address" : "500 Terry Francois, San Francisco"
  },
  {
  "switchProfileId" : null,
  "address" : "",
  "lng" : -122.098531723022,
  "model" : "MS220-8P",
  "mac" : "88:15:44:df:f3:af",
  "tags" : " recently-added ",
  "serial" : "QAAA-BBBB-CCCC",
  "networkId" : "L_646829496481099586",
  "lanIp" : "192.168.128.2",
  "lat" : 37.4180951010362
  }
]
```
So far, you have explored the Meraki Dashboard API using curl (also check Postman too) You first obtained the organization ID of the DevNet Sandbox Meraki account and then, based on that ID, you obtained all the networks that are part of the organization and then used one of the network IDs you obtained to find all the devices that are part of that specific network. This is, of course, just a subset of all the capabilities of the Meraki Dashboard API, wisit https://developer.cisco.com/meraki/ and check for more details.

There are two Meraki SDKs for the Dashboard API: one is Python based and the other is Node.js based. The Meraki Python SDK  was developed for Python 3 and implements a complete set of classes, methods, and functions to simplify how users interact with the Dashboard API in Python.

In order to get access to the SDK, you need to install the meraki-sdk module. As a best practice, always use virtual environments with all Python projects. Once a virtual environment is activated, you can run pip install meraki-sdk to get the latest version of the SDK. 

```
#! /usr/bin/env python
from meraki_sdk.meraki_sdk_client import MerakiSdkClient
#Cisco DevNet Sandbox Meraki API key
X_CISCO_MERAKI_API_KEY = '15da0c6ffff295f16267f88f98694cf29a86ed87'
#Establish a new client connection to the Meraki REST API
MERAKI = MerakiSdkClient(X_CISCO_MERAKI_API_KEY)
#Get a list of all the organizations for the Cisco DevNet account
ORGS = MERAKI.organizations.get_organizations()
for ORG in ORGS:
  print("Org ID: {} and Org Name: {}".format(ORG['id'], ORG['name']))
PARAMS = {}
PARAMS["organization_id"] = "549236" # Demo Organization "DevNet Sandbox"
#Get a list of all the networks for the Cisco DevNet organization
NETS = MERAKI.networks.get_organization_networks(PARAMS)
for NET in NETS:
  print("Network ID: {0:20s}, Name: {1:45s},Tags: {2:<10s}".format(NET['id'], NET['name'], str(NET['tags'])))
#Get a list of all the devices that are part of the Always On Network
DEVICES = MERAKI.devices.get_network_devices("L_646829496481099586")
for DEVICE in DEVICES:
  print("Device Model: {0:9s},Serial: {1:14s},MAC: {2:17}, Firmware:{3:12s}"\
  .format(DEVICE['model'], DEVICE['serial'], DEVICE['mac'], \
  DEVICE['firmware'])
```

After you instantiate the MerakiSdkClient class, you get an API client object that provides access to all the methods of the class. You can find the documentation for the Python SDK at https://developer.cisco.com/meraki/api/#/python/guides/python-sdk-quick-start. This documentation covers all the classes and methods, their parameters, and input and output values for the Python SDK implementation. Unlike with the curl and Postman examples earlier in this chapter, you do not need to determine the exact API resource that will return the information you are interested in; however, you do need to know how the MerakiSdkClient API class is organized and what methods are available.



# Cisco DNA Center: 
Cisco Digital Network Architecture (DNA) is an open, extensible, software-driven architecture from Cisco that accelerates and simplifies enterprise network operations. 
From a programmability perspective, Cisco DNA Center provides a set of REST APIs and SDKs through the Cisco DNA Center platform that are grouped in the following categories:

- **Intent API**: Intent API is a northbound REST API that exposes specific capabilities of the Cisco DNA Center platform. The main purpose of the Intent API is to simplify the process of creating workflows that consolidate multiple network actions into one.  The Intent API provides automation capabilities and simplified workflows for QoS policy configuration, software image management and operating system updates for all devices in the network, overall client health status, and monitoring of application health. Application developers and automation engineers can take advantage of this single northbound integration layer to develop tools and applications on top of the network.
  - **Know Your Network category:** This category contains API calls pertaining to sites, networks, devices, and clients:
    - With the Site Hierarchy Intent API, you can get information about, create, update, and delete sites as well as assign devices to a specific site. (Sites within Cisco DNA Center are logical groupings of network devices based on a geographic location or site.)
    - The Network Health Intent API retrieves data regarding network devices, their health, and how they are connected.
    - The Network Device Detail Intent API retrieves detailed information about devices. Different parameters can be passed to limit the scope of the information returned by the API, such as timestamp, MAC address, and UUID. Besides all the detailed information you can retrieve for all the devices in the network, you can also add, delete, update, or sync specified devices.
    - The Client Health Intent API returns overall client health information for both wired and wireless clients.
    - The Client Detail Intent API returns detailed information about a single client.
 - **Site Management category:** This category helps provision enterprise networks with zero-touch deployments and manage the activation and distribution of software images in the network:
    - The Site Profile Intent API gives you the option to provision NFV and ENCS devices as well as retrieve the status of the provisioning activities.
    - The Software Image Management (SWIM) API enables you to completely manage the lifecycle of software images running within a network in an automated fashion. With this API, you can retrieve information about available software images, import images into Cisco DNA Center, distribute images to devices, and activate software images that have been deployed to devices.
    - The Plug and Play (PnP) API enables you to manage all PnP-related workflows. With this API, you can create, update, and delete PnP workflows and PnP server profiles, claim and unclaim devices, add and remove virtual accounts, and retrieve information about all PnP-related tasks.
  - **Connectivity category:** This category contains APIs that provide mechanisms to configure and manage both non-fabric wireless and Cisco SDA wired fabric devices. For fabric devices, you can add and remove border devices to the fabric and get details about their status. For non-fabric wireless devices, you can create, update, and delete wireless SSIDs, profiles, and provisioning activities.
   - **Operational Tools category:** This category includes APIs for the most commonly used tools in the Cisco DNA Center toolbelt:
    - The Command Runner API enables the retrieval of all valid keywords that Command Runner accepts and allows you to run read-only commands on devices to get their real-time configuration.
    - The Network Discovery API provides access to the discovery functionalities of Cisco DNA Center. You can use this API to create, update, delete, and manage network discoveries and the credentials needed for them. You can also retrieve network discoveries, network devices that were discovered as part of a specific network discovery task, and credentials associated with these discoveries.
    - The Template Programmer API can be used to manage configuration templates. You can create, view, edit, delete, version, add commands, check contents for errors, deploy, and check the status of template deployments.
    - The Path Trace API provides access to the Path Trace application in Cisco DNA Center. Path Trace can be used to troubleshoot and trace application paths throughout the network and provide statistics at each hop. The API gives you access to initiating, retrieving, and deleting path traces.
    - The File API enables you to retrieve files such as digital certificates, maps, and SWIM files from Cisco DNA Center.
    - The Task API provides information about the network actions that are being run asynchronously. Each of these background actions can take from seconds to minutes to complete, and each has a task associated with it. You can query the Task API about the completion status of these tasks, get the task tree, retrieve tasks by their IDs, and so on.
    - The Tag API gives you the option of creating, updating, and deleting tags as well as assigning tags to specific devices. Tags are very useful in Cisco DNA Center; they are used extensively to group devices by different criteria. You can then apply policies and provision and filter these groups of devices based on their tags.

**The Cisco DNA Center platform APIs are rate limited to five API requests per minute.In Cisco DNA Center version 1.3, the REST API is not enabled by default. Therefore, you need to log in to DNA Center with a super-admin role account, navigate to Platform > Manage > Bundles, and enable the DNA Center REST API bundle.**
 You need to get authorized to the API and get the token that you will use for all subsequent API calls. The Cisco DNA Center platform API authorization is based on basic auth.  In the case of Cisco DNA Center, the username and password mentioned previously are base-64 encoded and then transmitted to the API service in the Authorization header. 
 ```
curl -X POST \
https://sandboxdnac2.cisco.com/dna/system/api/v1/auth/token \
-H 'Authorization: Basic ZGV2bmV0dXNlcjpDaXNjbzEyMyE='
```
 
 You verify the documentation and see that the authorization resource is /system/api/v1/auth/token and requires the API call to be POST. The token will be passed in the API calls through a header that is called X-Auth-Token.
 
 ```
 curl -X GET https://sandboxdnac2.cisco.com/dna/intent/api/v1/network-device \
-H 'X-Auth-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.
eyJzdWIiOiI1Y2U3MTJiMDhlZTY2MjAyZmEyZWI4ZjgiLCJhdXRoU291c-
mNlIjoiaW50ZXJuYWwiLCJ0ZW5hbnROYW1lIjoiVE5UMCIsInJvbGVzIjpbI-
jViNmNmZGZmNDMwOTkwMDA4OWYwZmYzNyJdLCJ0ZW5hbnRJZCI6IjViNmNmZG-
ZjNDMwOTkwMDA4OWYwZmYzMCIsImV4cCI6MTU2NjYwODAxMSwidXNlcm5hbWUiOi-
JkZXZuZXR1c2VyIn0.YXc_2o8FDzSQ1YBhUxUIoxwzYXXWYeNJRkB0oKBlIHI'
```

- **Integration API:** One of the main goals of the Cisco DNA Center platform is to **simplify and streamline end-to-end IT processes**. The Integration API was created for exactly this purpose. Through this API, Cisco DNA Center platform publishes network data, events, and notifications to external systems and at the same time can consume information from these connected systems. **Integrations with IT service management systems** like Service Now, BMC Remedy, and other ticketing systems are supported. Automatic ticket creation and assignment based on network issues that are flagged by Cisco DNA Center are now possible. **IP Address Management (IPAM) integrations are also supported** by the Integration API. It is possible to seamlessly import IP address pools of information from IPAM systems such as Infoblox and BlueCat into Cisco DNA Center. **Synchronization of IP pool/subpool information between Cisco DNA Center and IPAM systems is also supported**. Through the Integration API that Cisco DNA Center provides, developers can integrate with any third-party IPAM solution. Data as a service (DaaS) APIs that are part of the Integration API allow **Cisco DNA Center to publish insights and data to external tools** such as Tableau and similar reporting solutions. IT administrators have the option to build dashboards and extract business-relevant insights. The Integration API is also used for **cross-domain integrations with other Cisco products**, such as Cisco Meraki, Cisco Stealthwatch, and Cisco ACI. The idea is to deliver a consistent intent-based infrastructure across the data center, WAN, and security solutions.
- **Multivendor SDK:** Cisco DNA Center allows customers to have their non-Cisco devices managed by DNA Center through a multivendor SDK. Cisco DNA Center communicates with third-party devices through device packages. The device packages are developed using the multivendor SDK and implement southbound interfaces based on CLI, SNMP, or NETCONF.
- **Events and notifications:** Cisco DNA Center also provides webhooks for events and notifications that are generated in the network or on the Cisco DNA Center appliance itself. This completes the feedback loop in the sense that a notification generated by Cisco DNA Center is interpreted by a third-party custom application and acted upon by sending either an Intent API or Integration API call back to Cisco DNA Center to either remedy or modify the network, based on the desired business outcome. This mechanism of publishing events and notifications also saves on processing time and resources; before this capability existed, the custom application had to poll continuously to get the status of an event. By subscribing through the webhook, polling can now be avoided entirely, and the custom application receives the status of the event right when it gets triggered.

Next let's explore the Cisco DNA Center Python SDK. The SDK has been developed for Python 3 and maps all the Cisco DNA Center APIs into Python classes and methods to make it easier for developers to integrate with and expand the functionality of Cisco DNA Center. Installing the SDK is as simple as issuing the command **pip install dnacentersdk** from the command prompt.


```
#! /usr/bin/env python
from dnacentersdk import api
# Create a DNACenterAPI connection object;
# it uses DNA Center sandbox URL, username and password
DNAC = api.DNACenterAPI(username="devnetuser",password="Cisco123!",base_url="https://sandboxdnac2.cisco.com")
# Find all devices
DEVICES = DNAC.devices.get_device_list()
# Print select information about the retrieved devices
print('{0:25s}{1:1}{2:45s}{3:1}{4:15s}'.format("Device Name", "|", "Device Type", "|", "Up Time"))
print('-'*95)
for DEVICE in DEVICES.response:
     print('{0:25s}{1:1}{2:45s}{3:1}{4:15s}'.format(DEVICE.hostname, "|", DEVICE.type, "|", DEVICE.upTime))
print('-'*95)
# Get the health of all clients on Thursday, August 22, 2019 8:41:29 PM GMT
CLIENTS = DNAC.clients.get_overall_client_health(timestamp="1566506489000")
# Print select information about the retrieved client health statistics
print('{0:25s}{1:1}{2:45s}{3:1}{4:15s}'.format("Client Category", "|","Number of Clients", "|", "Clients Score"))
print('-'*95)
for CLIENT in CLIENTS.response:
    for score in CLIENT.scoreDetail:
      print('{0:25s}{1:1}{2:<45d}{3:1}{4:<15d}'.format(score.scoreCategory.value, "|", score.clientCount, "|", score.scoreValue))
print('-'*95)
```
First, this example imports the api class from dnacentersdk. Next, it instantiates the api class and creates a connection to the always-on Cisco DevNet Sandbox DNA Center instance and stores the result of that connection in a variable called DNAC. If the connection was successfully established, the DNAC object has all the API endpoints mapped to methods that are available for consumption. DNAC.devices.get_device_list() provides a list of all the devices in the network and stores the result in the DEVICES dictionary. The same logic applies to the client health status. DNAC.clients.get_overall_client_health(timestamp='1566506489000') returns a dictionary of health statuses for all the clients at that specific time, which translates to Thursday, August 22, 2019 8:41:29 PM GMT. When the data is extracted from the API and stored in the variables named DEVICES for all the network devices and CLIENTS for all the client health statuses, a rudimentary table is displayed in the console, with select information from both dictionaries. For the DEVICES variable, only the device name, device type, and device uptime are displayed, and for the CLIENTS variable, only the client health category, number of clients, and client score for each category are displayed.

# Cisco SD-WAN: 
Cisco SD-WAN (Software-Defined Wide Area Network) is a cloud-first architecture for deploying WAN connectivity. Wide-area networks have been deployed for a long time, and many lessons and best practices have been learned throughout the years. Applying all these lessons to software-defined networking (SDN) resulted in the creation of Cisco SD-WAN. An important feature of SDN is the separation of the control plane from the data plane. The control plane includes a set of protocols and features that a network device implements so that it can determine which network path to use to forward data traffic.(The data plane includes the protocols and features that a network device implements to forward traffic to its destination as quickly as possible.)

SDN separates the functionality of the control plane and data plane in different devices, and several benefits result. 
- First, the cost of the resulting network should be lower as not all network devices have to implement expensive software and hardware features to accommodate both a control plane and data plane.
- Second, the convergence of this new network, which is the amount of time it takes for all devices to agree on a consistent view of the network.

Cisco currently has two SD-WAN offerings. The first one, based on the Viptela acquisition, is called Cisco SD-WAN; the second one, based on the Meraki acquisition, is called Meraki SD-WAN. 

- **vManage:** Cisco vManage is a centralized network management system that provides a GUI and REST API interface to the SD-WAN fabric. You can easily manage, monitor, and configure all Cisco SD-WAN components through this single pane of glass.
- **vSmart:** Cisco vSmart is the brains of the centralized control plane for the overlay SD-WAN network. It maintains a centralized routing table and centralized routing policy that it propagates to all the network Edge devices through permanent DTLS tunnels.
- **vBond:** Cisco vBond is the orchestrator of the fabric. It authenticates the vSmart controllers and the vEdge devices and coordinates connectivity between them. The vBond orchestrator is the only component in the SD-WAN fabric that needs public IP reachability to ensure that all devices can connect to it.
- **vEdge:** Cisco vEdge routers, as the name implies, are Edge devices that are located at the perimeter of the fabric, such as in remote offices, data centers, branches, and campuses. They represent the data plane and bring the whole fabric together and route traffic to and from their site across the overlay network.

All the components of the Cisco SD-WAN fabric run as virtual appliances, and the vEdges are also available as hardware routers. Separating the WAN fabric this way makes it more scalable, faster to converge, and cheaper to deploy and maintain. On top of a transport-independent underlay that supports all types of WAN circuits (MPLS, DSL, broadband, 4G, and so on), an overlay network is being built that runs OMP (Overlay Management Protocol). Much like BGP, OMP propagates throughout the network all the routing information needed to forward data according to the routing policies configured in vManage.

Cisco vManage provides a REST API interface that exposes the functionality of the Cisco SD-WAN software and hardware features. The API resources that are available through the REST interface are grouped in the following collections:

- **Administration:** For management of users, groups, and local vManage instance
- **Certificate Management:** For management of SSL certificates and security keys
- **Configuration:** For creation of feature and device configuration templates and creation and configuration of vManage clusters
- **Device Inventory:** For collecting device inventory information, including system status
- **Monitoring:** For getting access to status, statistics, and related operational information about all the devices in the network every 10 minutes from all devices
- **Real-Time Monitoring:** For gathering real-time monitoring statistics and traffic information approximately once per second
- **Troubleshooting Tools:** For API calls used in troubleshooting, such as to determine the effects of applying a traffic policy, updating software, or retrieving software version information

Cisco vManage exposes a self-documenting web interface for the REST API, based on the OpenAPI specification. This web interface is enabled by default and can be accessed at https://vManage_IP_or_hostname:port/apidocs. vManage_IP_or_hostname is the IP address or hostname of the Cisco vManage server, and the port is 8443 by default.

The API documentation can be found at https://sdwan-docs.cisco.com/Product_Documentation/Command_Reference/Command_Reference/vManage_REST_APIs. At this link, you can find all the information needed on how to interact with the REST API, all the resources available, and extensive explanations.

```
curl -c - -X POST -k \
https://sandboxsdwan.cisco.com:8443/j_security_check \
-H 'Content-Type: application/x-www-form-urlencoded' \
-d 'j_username=devnetuser&j_password=Cisco123!'
```
The status code of the response should be 200 OK and the JSESSIONID cookie should included. Further examples throught the documentation.


The script was developed using Python 3.7.4 and version 2.22.0 of the requests library. The json library that comes with Python 3.7.4 was also used to deserialize and load the data returned from the REST API into a Python object; in this case, that object is a list. In this code, first, the import keyword makes the two libraries requests and json available for use within the script. Since the connection in the script is made to an instance of vManage that is in a sandbox environment and that uses a self-signed SSL certificate, the third and fourth lines of the script disable the warning messages that are generated by the requests library when connecting to REST API endpoints that are secured with self-signed SSL certificates. Next, the script specifies the vManage hostname and the username and password for this instance; this example uses the same vManage server used earlier in this chapter. The code then specifies the base URL for the vManage REST API endpoint: https://sandboxsdwan.cisco.com:8443. The code shows the authentication resource (j_security_check) and the login credentials, and then the login URL is built as a combination of the base URL and the authentication API resource. In the next line, a new request session instance is created and stored in the SESS variable.

```
#! /usr/bin/env python
import json
import requests
from requests.packages.urllib3.exceptions import InsecureRequestWarning
requests.packages.urllib3.disable_warnings(InsecureRequestWarning)
# Specify Cisco vManage IP, username and password
VMANAGE_IP = 'sandboxsdwan.cisco.com'
USERNAME = 'devnetuser'
PASSWORD = 'Cisco123!'
BASE_URL_STR = 'https://{}:8443/'.format(VMANAGE_IP)
# Login API resource and login credentials
LOGIN_ACTION = 'j_security_check'
LOGIN_DATA = {'j_username' : USERNAME, 'j_password' : PASSWORD}
# URL for posting login data
LOGIN_URL = BASE_URL_STR + LOGIN_ACTION
# Establish a new session and connect to Cisco vManage
SESS = requests.session()
LOGIN_RESPONSE = SESS.post(url=LOGIN_URL, data=LOGIN_DATA, verify=False)
# Get list of devices that are part of the fabric and display them
DEVICE_RESOURCE = 'dataservice/device'
# URL for device API resource
DEVICE_URL = BASE_URL_STR + DEVICE_RESOURCE
DEVICE_RESPONSE = SESS.get(DEVICE_URL, verify=False)
DEVICE_ITEMS = json.loads(DEVICE_RESPONSE.content)['data']
print('{0:20s}{1:1}{2:12s}{3:1}{4:36s}{5:1}{6:16s}{7:1}{8:7s}'.format("Host-Name", "|", "Device Model", "|", "Device ID", "|", "System IP", "|", "Site ID"))
print('-'*105)
for ITEM in DEVICE_ITEMS:
  print('{0:20s}{1:1}{2:12s}{3:1}{4:36s}{5:1}{6:16s}{7:1}{8:7s}'.format(ITEM['host-name'], "|", ITEM['device-model'], "|", ITEM['uuid'], "|", ITEM['system-ip'], "|", ITEM['site-id']))
print('-'*105)
# Get list of device templates and display them
TEMPLATE_RESOURCE = 'dataservice/template/device'
# URL for device template API resource
TEMPLATE_URL = BASE_URL_STR + TEMPLATE_RESOURCE
TEMPLATE_RESPONSE = SESS.get(TEMPLATE_URL, verify=False)
TEMPLATE_ITEMS = json.loads(TEMPLATE_RESPONSE.content)['data']
print('{0:20s}{1:1}{2:12s}{3:1}{4:36s}{5:1}{6:16s}{7:1}{8:7s}'.format("Template Name", "|", "Device Model", "|", "Template ID", "|", "Attached devices", "|", "Template Version"))
print('-'*105)
for ITEM in TEMPLATE_ITEMS:
  print('{0:20s}{1:1}{2:12s}{3:1}{4:36s}{5:1}{6:<16d}{7:1}{8:<7d}'\
    .format(ITEM['templateName'], "|", ITEM['deviceType'], "|", \
      ITEM['templateId'], "|"" ITEM['devicesAttached'], "|", ITEM['templateAttached']))
print('-'*105)
```








