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

- Intent API
- Integration API
- Multivendor SDK
- Events and notifications


# Cisco SD-WAN: 
This section covers Cisco SD-WAN and the REST APIs exposed through Cisco vManage.
