## Application Programming Interfaces (APIs)
For communicating with and configuring networks, software developers commonly use application programming interfaces (APIs). APIs are mechanisms used to communicate with applications and other software. They are also used to communicate with various components of a network through software. A developer can use APIs to configure or monitor specific components of a network. Although there are multiple different types of APIs, this chapter focuses on two of the most common APIs: northbound and southbound APIs. The following sections explain the differences between these two API types through the lens of network automation.

### Northbound APIs

**Northbound APIs are often used for communication from a network controller to its management software**. For example, Cisco DNA Center has a software graphical user interface (GUI) that is used to manage its own network controller. Typically, when a network operator logs into a controller to manage the network, the information that is passed to the management software leverages a northbound REST-based API. Best practices suggest that the traffic should be encrypted using TLS between the software and the controller. Most types of APIs have the ability to use encryption to secure the data in flight.

### Southbound APIs

If a network operator makes a **change to a switch's configuration in the management software of the controller, those changes will then be pushed down to the individual devices using a southbound API**. These devices can be routers, switches, or even wireless access points. APIs interact with the components of a network through the use of a programmatic interface. Southbound APIs can modify more than just the data plane on a device.

#Synchronous Versus Asynchronous APIs

APIs can handle transactions either in a synchronous manner or an asynchronous manner. A **synchronous API causes an application to wait for a response from the API in order to continue processing data or function normally.** This can lead to interruptions in application processing as delay in responses or failed responses could cause the application to hang or stop performing the way it was intended to work. This might occur, for example, if an application relies on some piece of information to be retrieved from another API before it can continue functioning. For example, uploading videos to YouTube was originally a synchronous use case.  **Asynchronous APIs do exactly the opposite of synchronous APIs in that they do not wait until a response is received prior to continuing to function and process other aspects of data.** Asynchronous APIs provide a callback function so that the API response can be sent back at another time, without the application having to wait for the entire transaction to complete. As an example of an asynchronous API, today you can upload a video to YouTube, and while it's uploading, users can change the title, add hashtags, and even retrieve the URL to which the video will be posted once it is finished being uploaded.

**In summary, the main difference between synchronous and asynchronous APIs is that a synchronous API waits for other aspects of the code to complete prior to moving on and processing additional code. An asynchronous API, on the other hand, provides the ability to continue processing code and provides a callback so that an application doesn't have to wait for the API call to complete before it can continue processing other API calls.**

## Representational State Transfer (REST) APIs

An API that uses REST is often referred to a RESTful API. **RESTful APIs use HTTP methods to gather and manipulate data.** Because there is a defined structure for how HTTP works, HTTP offers a consistent way to interact with APIs from multiple vendors. REST uses different HTTP functions to interact with data. 

HTTP functions are very similar to the functions that most applications and databases use to store or alter data, whether it is stored in a database or within an application. These functions are called CRUD functions; **CRUD is an acronym that stands for CREATE, READ, UPDATE, and DELETE**. For example, in an SQL database, the CRUD functions are used to interact with or manipulate the data stored in the database. 


|Function|Action|Use Case|
|-------------|------|--------|
|**HTTP**|Functions and Sample Use Cases||
|GET|Requests data from a destination|Viewing a website|
|POST|Submits data to a specific destination|Submitting login credentials|
|PUT|Replaces data at a specific destination|Updating an NTP server|
|PATCH|Appends data to a specific destination|Adding an NTP server|
|DELETE|Removes data from a specific destination|Removing an NTP server|
|**CRUD**|Functions and Sample Use Cases||
|CREATE|Inserts data inside a database or an application|Creating a customer's home address in a database|
|READ|Retrieves data from a database or an application|Pulling up a customer's home address from a database|
|UPDATE|Modifies or replaces data in a database or an application|Changing a street address stored in a database|
|DELETE|Removes data from a database or an application|Removing a customer from a database|

## RESTful API Authentication
Many APIs require authentication; such APIs are just like devices in that the user needs to authenticate to gain access to utilize the APIs. Once a user has authenticated, any changes that a developer has access to make via the API are then able to impact the application. This means if a RESTful API call is used to delete data, that data will be removed from the application or controller just as if a user were logged into the device via the CLI and deleted it. 

### Basic Authentication

Basic authentication is one of the simplest and most common authentication methods used in APIs. In the context of an HTTP transaction, basic access authentication is a method for an HTTP user agent (e.g. a web browser) to provide a user name and password when making a request. In basic HTTP authentication, a request contains a header field in the form of **Authorization: Basic \<credentials>, where credentials is the Base64 encoding of ID and password joined by a single colon :.**

The downfall of basic authentication is that the credentials might passed unencrypted. This means that if the transport is simple HTTP, it is possible to sniff the traffic and capture the username and password with little to no effort. The lack of encryption means that the credentials are in simple plaintext base 64 encoding in the HTTP header. However, basic authentication is more commonly used with SSL or TLS to prevent such attacks.

[https://en.wikipedia.org/wiki/Basic_access_authentication](https://en.wikipedia.org/wiki/Basic_access_authentication)

Another big issue with basic authentication is that the password is sent back and forth with each request, which increases the opportunity for an attacker to capture the traffic containing the password. 

### API Keys
An application programming interface key (API key) is a unique identifier used to authenticate a user, developer, or calling program to an API. It is intended to be a pre-shared secret and should not be well known or easy to guess because it functions just like a password. Anyone with this key can access the API in question and can potentially cause a major outage and gain access to critical or sensitive data. 

(https://en.wikipedia.org/wiki/Application_programming_interface_key)

An API key can be passed to the server in three different ways:
1. String

 This type of API key is sent with every API call and is often used as a one-off method of authentication. When you're looking to do multiple API calls, it isn't convenient to manually enter the API key string every time. This is where the request header or cookie options come into play.

```GET /something?api_key=abcdef12345```

2. Request header

Request headers are frequently used when a user is making multiple API calls and doesn't want to keep having to put the API key into each API individually. This approach is typically seen in Postman and Python scripts. The header must include the string or token in the header of each API call. 

```GET /something HTTP/1.1
...
<header>
X-API-Key: abcdef12345
```

3. Cookie

One of the most common methods for recurring API calls is to use cookies. A cookie stores the API key string and can be reused and stored over and over. This is synonymous with a header. Example 6-3 shows an API key cookie that uses the same key as the previous examples.
```
GET /something HTTP/1.1
...
<header>
Cookie: X-API-KEY=abcdef12345
```

## Simple Object Access Protocol (SOAP)
## Remote-Procedure Calls (RPCs)
