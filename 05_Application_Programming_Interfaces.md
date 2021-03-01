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
4. Custom token
A custom token allows a user to enter his or her username and password once and receive a unique auto-generated and encrypted token. The user can then use this token to access protected pages or resources instead of having to continuously enter the login credentials. Tokens can be time bound and set to expire after a specific amount of time has passed, thus forcing users to reauthenticate by reentering their credentials. A token is designed to show proof that a user has previously authenticated. It simplifies the login process and reduces the number of times a user has to provide login credentials. A token is stored in the user's browser and gets checked each time the user tries to access information requiring authentication. Once the user logs out of the web browser or website, the token is destroyed so it cannot be compromised.


## Simple Object Access Protocol (SOAP)
Simple Object Access Protocol (SOAP) is used to access web services. Although HTTP is the most commonly deployed transport for SOAP, SOAP can use either Simple Mail Transfer Protocol (SMTP) or HTTP. **SOAP is used to exchange data between applications that were built on different programming languages**, such as Java, .NET, and PHP. SOAP greatly simplifies the life of a developer, eliminating the need to know how to develop in each of these specific programming languages. It makes it possible to exchange data between these applications in a more simplified manner, without requiring a developer to be expert in all the different languages. **SOAP is based on XML.** Because most programming languages today have libraries for working with XML, **SOAP can act as an intermediary specification between the different applications.**

SOAP uses XML to communicate between web services and clients. Because SOAP is platform and operating system independent, it can work with both Windows and Linux platforms. SOAP messages, which typically consist of the following four main components, are sent between the web applications and the clients.

Soap message format:
- Envelope
- Header
- Body
- Fault (optional)

The SOAP **envelope encloses the XML data and identifies it as a SOAP message**. The **envelope indicates the beginning and the end of the SOAP message**. The next portion of a SOAP message is the SOAP header, and it can contain multiple header blocks. **Header blocks are targeted to specific SOAP receiver nodes.** If a SOAP message contains a header, it must come before the body element. The SOAP **body contains the actual message that is designated for the SOAP receiver.** Every SOAP **envelope must contain at least one body element**. Typically, SOAP messages are automatically generated by the web service when it's called by the client. 


Another potentially beneficial aspect of SOAP is that because it primarily uses HTTP, it is efficient in passing through firewalls without requiring that any additional ports be allowed or open for the web service traffic to be permitted. This can save time and reduce some operational overhead. To reiterate, the benefit of SOAP is its capability to work between different languages while using a simple common HTTP and XML structure. 

SOAP message
```
POST /InStock HTTP/1.1
Host: www.example.org
Content-Type: application/soap+xml; charset=utf-8
Content-Length: 299
SOAPAction: "http://www.w3.org/2003/05/soap-envelope
<?xml version="1.0"?>
<soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" xmlns:m="http://
www.example.org">
 <soap:Header>
 </soap:Header>
  <soap:Body>
   <m:GetStockPrice>
    <m:StockName>CSCO</m:StockName>
   </m:GetStockPrice>
 </soap:Body>
</soap:Envelope>
```
The World Wide Web Consortium (W3C) recommends using the **current SOAP specification, version 1.2.** The previous version of SOAP is 1.1. Although it is possible for a SOAP node to support both versions of the protocol, a protocol binding must be used for the version of SOAP that the client intends to use.

SOAP fault options

|Fault Element|Description|Optional|
|-------------|-----------|--------|
|faultCode|Specifies the fault code of an error|No|
|faultString|Describes an error|No|
|faultActor|Specifies who caused a fault|Yes|
|detail|Applies specific error messages|Yes|

Table shows the options available in SOAP version 1.2. **faultString provides a description of an error message** that is generated. This is **not an optional field**; rather, it is mandatory in the communications between the client and the web service. **faultActor specifies which node caused a fault**. Although this field would provide some additional information related to who caused the fault at hand, this field is optional. The **detail element provides application-specific error messages**; that is, this element is populated with information provided by the application. SOAP fault messages can contain a variety of **faultCode options, which indicate what errors were generated as well as potentially who caused each error (the sender or receiver).** 

|SOAP Fault Code|Description|
|---------------|-----------|
|VersionMismatch|The faulting node found an invalid element information item instead of the expected envelope element information item. The namespace, local name, or both did not match the envelope element information item required by this recommendation.|
|MustUnderstand|This is a child element of the SOAP header. If this attribute is set, any information that was not understood triggers this fault code.|
|DataEncodingUnknown|A SOAP header block or SOAP body child element information item targeted at the faulting SOAP node is scoped.|
|Sender|The message was incorrectly formed or did not contain the information needed to succeed. For example, the message might have lacked the proper authentication or payment information. This code generally indicates that the message is not to be resent without change.|
|Receiver|The message could not be processed for reasons attributable to the processing of the message rather than to the contents of the message itself. For example, processing could include communicating with an upstream SOAP node, which did not respond. The message could succeed, however, if resent at a later point in time.|

SOAP fault
```
<env:Envelope xmlns:env="http://www.w3.org/2003/05/soap-envelope"
                    xmlns:m="http://www.example.org/timeouts"
                    xmlns:xml="http://www.w3.org/XML/1998/namespace">
 <env:Body>
  <env:Fault>
   <env:Code>
     <env:Value>env:Sender</env:Value>
     <env:Subcode>
     <env:Value>m:MessageTimeout</env:Value>
    </env:Subcode>
   </env:Code>
   <env:Reason>
    <env:Text xml:lang="en">Sender Timeout</env:Text>
   </env:Reason>
   <env:Detail>
    <m:MaxTime>P5M</m:MaxTime>
  </env:Detail>
 </env:Fault>
 </env:Body>
</env:Envelope>
```
## Remote-Procedure Calls (RPCs)

**Remote-procedure calls (RPCs) make it possible to execute code or a program on a remote node in a network**. RPCs behave as if the code were executed locally on the same local node, even though the code is executed on a remote address space, such as another system on the network. Most remote and local calls are very similar in nature and can be distinguished from one another based on whether they are local or remote. **RPCs are sometimes also known as function or subroutine calls**. Using an RPC is a very common way of executing specific commands, such as executing GET or POST operations to a set API or URL.

When a client sends a request message, the RPC translates it and then sends it to the server. A request may be a procedure or a function call destined to a remote server. When a server receives the request, it sends back a response to the client. While this communication is happening, the client is blocked, allowing the server time to process the call. Once the call is processed and a response has been sent back to the client, the communication between the client and server is unblocked so the client can resume executing the procedure call. This can be considered a security mechanism to prevent the flooding of RPCs to brute-force the server and cause denial-of-service (DoS) attacks or exhaustion of resources. Figure 6-8 showcases the high-level RPC communications between a client and a server.

As mentioned earlier in this section, an RPC call is blocked during the waiting periods. Once a procedure is executed and the response is sent from the server and received on the client, the execution of the procedure continues. (This means that RPC calls are typically synchronous. There are also asynchronous RPC calls, but the focus of this section is on synchronous RPC calls.)

Now that the high-level communications of RPC have been covered, let's look at an example of an RPC request message. There are different versions of RPC messages. However, the most common is XML-RPC; XML-RPC was also the most common version prior to SOAP becoming available. Example 6-6 shows a simple RPC call with XML-RPC that uses a GET to retrieve the name of the 21st state added to the United States.

```
Click here to view code image
<?xml version="1.0"?>
<methodCall>
 <methodName>examples.getStateName</methodName>
 <params>
  <param>
   <value><i4>21</i4></value>
  </param>
 </params>
</methodCall>
```
You can see that the format of XML is very similar to that of SOAP, making these messages simple for humans to read and digest and also to build. An example of an XML-RPC reply or response message, in which the response to the GET message from Example 6-6 is Illinois.
```
<?xml version="1.0"?>
<methodResponse>
  <params>
   <param>
    <value><string>Illinois</string></value>
   </param>
 </params>
</methodResponse>
```
