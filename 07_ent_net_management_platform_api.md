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

The Cisco Meraki Dashboard API uses the base URL **https://api.meraki.com/api/v0**. Keep in mind that the API will evolve, and different versions will likely be available in the future. Always check the API documentation for the latest information on all Cisco APIs, including the Meraki APIs, at https://developer.cisco.com.



# Cisco DNA Center: 
This section covers Cisco DNA Center and the REST APIs that it publicly exposes.
# Cisco SD-WAN: 
This section covers Cisco SD-WAN and the REST APIs exposed through Cisco vManage.
