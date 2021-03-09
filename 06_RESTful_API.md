## RESTful API Fundamentals
An application programming interface (API) is a set of functions and procedures intended to be used as an interface for software components to communicate with each other. An API may be for a web app, an operating system, a database system, computer hardware, or any software library. A common example of an API is the Google Maps API, which lets you interface with Google Maps so that you can display maps in your application, query locations, and so on. 

### API Types

APIs can be broadly classified into three categories, based on the type of work that each one provides:
- **Service API:** In a service API, an application can call on another application to solve a particular problem. Usually these systems can exist independently. For example, in a payment system, an application can call the API to accept payments via credit cards. As another example, with a user-management system, an application can call an API to validate and authenticate users.
images
- **Information API:** An information API allows one application to ask another application for information. Information in this context can refer to data gathered over time, telemetry data, or a list of devices that are currently connected. 
images
- **Hardware API:** Application developers use hardware APIs to gain access to the features of hardware devices. Usually these APIs encompass some kind of hardware or sensors, and an application can call this kind of API to get the GPS location or real-time sensor data such as temperature or humidity. 

Regardless of how they are accessed, APIs are designed to interact through a network. Because the most widely used communications network is the Internet, most APIs are designed based on web standards. Not all remote APIs are web APIs, but it's fair to assume that web APIs are remote.

#### HTTP basics

A web browser is a classic example of an HTTP client. Communication in HTTP centers around a concept called the request/response cycle, in which the client sends the server a request to do something. The server, in turn, sends the client a response saying whether or not the server can do what the client asked. 

In HTTP, in order to make a successful request to the server, the client needs to include four items:

- URL (uniform resource locator)
- Method
- List of headers
- Body
- The following sections look at each of these items in detail.

##### Uniform Resource Locator (URL)

An URL is similar to a house address in that it defines the location where a service resides on the Internet. A URL typically has four components.
1. Protocol
2. Server/host address
3. Resource
4. Parameters

The **server or host address is the unique server** name, **/api/rooms/livingroom defines a resource** to access, and **lights?state=ON is the parameter** to send in order to take some action.

##### Method

HTTP defines a set of request methods. A client can use one of these request methods to send a request message to an HTTP server.
|Method|Explanation|
|------|-----------|
|GET|A client can use a GET request to get a web resource from the server.|
|HEAD|A client can use a HEAD request to get the header that a GET request would have obtained. Because the header contains the last-modified date of the data, it can be used to check against the local cache copy.|
|POST|A client can use a POST request to post data or add new data to the server.|
|PUT|A client can use a PUT request to ask a server to store or update data.|
|PATCH|A client can use a PATCH request to ask a server to partially store or update data.|
|DELETE|A client can use a DELETE request to ask a server to delete data.|
|TRACE|A client can use a TRACE request to ask a server to return a diagnostic trace of the actions it takes.|
|OPTIONS|A client can use an OPTIONS request to ask a server to return a list of the request methods it supports.|
|CONNECT|A client can use a CONNECT request to tell a proxy to make a connection to another host and simply reply with the content, without attempting to parse or cache it. This request is often used to make SSL connection through the proxy.|

##### REST Methods and CRUD

As you have seen, REST is an architectural paradigm that allows developers to build RESTful services. These RESTful applications make use of HTTP requests for handling all four CRUD operations: CREATE, READ, UPDATE, and DELETE. These four operations are the operations most commonly used in manipulating data. The HTTP methods map in a one-to-one way to the CRUD operations.

|HTTP Method|Operation|Explanation|Example|
|-----------|---------|-----------|-------|
|POST|CREATE|Used to create a new object or resource.|Example: Add new room to a house|
|GET|READ|Used to retrieve resource details from the system.|Example: Get a list of all the rooms or all the details of one room|
|PUT|UPDATE|Typically used to replace or update a resource. Can be used to modify or create a resource.|Example: Update details of a room|
|PATCH|UPDATE|Used to modify some details about a resource.|Example: Change the dimensions of a room|
|DELETE|DELETE|Used to remove a resource from the system.|Example: Delete a room from a house.|

##### GET
GET is the most common HTTP request method. A client can use the GET request method to request a resource from an HTTP server. GET requests, which have special qualities, fetch information, and that's it; they have no side effects, make no modifications to the system, create nothing, and destroy nothing. GET requests should, in other words, be safe and idempotent. (Idempotent means that no matter how many times you perform an action, the state of the system you're dealing with remains the same.)

A GET request message has the following components:
- **GET:** The keyword GET must be all uppercase.
- **Request URI**: Specifies the path of the resource requested, which must begin from the root / of the document base directory.
- **HTTP version**: Either HTTP/1.0 or HTTP/1.1. This client negotiates the protocol to be used for the current session. For example, the client may request to use HTTP/1.1. If the server does not support HTTP/1.1, it may inform the client in the response to use HTTP/1.0.
- **Request headers (optional)**: The client can use optional request headers (such as accept and accept language) to negotiate with the server and ask the server to deliver the preferred contents (such as in the language the client prefers).
- **Request body (optional)**: A GET request message has an optional request body, which contains the query string (explained later in this chapter).

##### POST
The POST request method is used to post additional data to the server (for example, submitting HTML form data or uploading a file). Issuing an HTTP URL from the browser always triggers a GET request. To trigger a POST request, you can use an HTML form with attribute method='post' or write your own code. For submitting HTML form data, the POST request is the same as the GET request except that the URL-encoded query string is sent in the request body rather than appended behind the request URI.

- **POST**: The keyword POST must be all uppercase.
- **Request URI**: Specifies the path of the resource requested, which must begin from the root / of the document base directory.
- **HTTP version**: Either HTTP/1.0 or HTTP/1.1. This client negotiates the protocol to be used for the current session. For example, the client may request to use HTTP/1.1. If the server does not support HTTP/1.1, it may inform the client in the response to use HTTP/1.0.
- **Request headers (optional)**: The client can use optional request headers, such as content type and content length to inform the server of the media type and the length of the request body, respectively.
- **Request body (optional)**: A POST request message has an optional request body, which contains the query string (explained later in this chapter).

##### HTTP Headers

The HTTP headers and parameters provide of a lot of information that can help you trace issues when you encounter them. HTTP headers are an essential part of an API request and response as they represent the metadata associated with the API request and response. Headers carry information for the following:

- Request and response body
- Request authorization
- Response caching
- Response cookies

In addition, HTTP headers have information about HTTP connection types, proxies, and so on. Most of these headers are for managing connections between a client, a server, and proxies. **Headers are classified as request headers and response headers.** You have to set the request headers when sending a request API and have to set the assertion against the response headers to ensure that the correct headers are returned.

**Request Headers**:The request headers appear as name:value pairs. Multiple values, separated by commas, can be specified as follows:
```
request-header-name: request-header-value1, request-header-value2, ...
```

```
Host: myhouse.cisco.com
Connection: Keep-Alive
Accept: image/gif, image/jpeg, */* <<< like this
Accept-Language: us-en, fr, cn <<<< like this
```

**Response Headers:** The response headers also appear as name:value pairs. As with request headers, multiple values can be specified as follows:
```
response-header-name: response-header-value1, response-header-value2, ...
```

```
Content-Type: text/html
Content-Length: 35
Connection: Keep-Alive
Keep-Alive: timeout=15, max=100
```
The response message body contains the resource data requested.

- Authorization: Carries credentials containing the authentication information of the client for the resource being requested.
- WWW-Authenticate: This is sent by the server if it needs a form of authentication before it can respond with the actual resource being requested. It is often sent along with response code 401, which means "unauthorized".
- Accept-Charset: This request header tells the server which character sets are acceptable by the client.
- Content-Type: This header indicates the media type (text/HTML or application/JSON) of the client request sent to the server by the client, which helps process the request body correctly.
- Cache-Control: This header is the cache policy defined by the server. For this response, a cached response can be stored by the client and reused until the time defined in the Cache-Control header.


**Response Codes**: The first line of a response message (that is, the status line) contains the response status code, which the server generates to indicate the outcome of the request. Each status code is a three-digit number:

- 1xx (informational): The request was successfully received; the server is continuing the process.
- 2xx (success): The request was successfully received, understood, accepted, and serviced.
- 3xx (redirection): Further action must be taken to complete the request.
- 4xx (client error): The request cannot be understood or is unauthorized or the requested resource could not be found.
- 5xx (server error): The server failed to fulfill a request.

|Status Code|Meaning|Explanation|
|-----------|-------|-----------|
|100|Continue|The server received the request and is in the process of giving the response.|
|200|Okay|The request is fulfilled.|
|301|Move permanently|The resource requested has been permanently moved to a new location. The URL of the new location is given in the Location response header. The client should issue a new request to the new location, and the application should update all references to this new location.|
|302|Found and redirect (or move temporarily)|This is the same as code 301, but the new location is temporary in nature. The client should issue a new request, but applications need not update the references.|
|304|Not modified|In response to the if-modified-since conditional GET request, the server notifies that the resource requested has not been modified.|
|400|Bad request|The server could not interpret or understand the request; there is probably a syntax error in the request message.|
|401|Authentication required|The requested resource is protected and requires the client's credentials (username and password). The client should resubmit the request with the appropriate credentials (username and password).|
|403|Forbidden|The server refuses to supply the resource, regardless of the identity of the client.|
|404|Not found|The requested resource cannot be found on the server.|
|405|Method not allowed|The request method used (for example, POST, PUT, DELETE) is a valid method. However, the server does not allow that method for the resource requested.|
|408|Request timeout|The request sent to the server took longer than the website's server was prepared to wait.|
|414|Request URI too large|The URI requested by the client is longer than the server is willing to interpret.|
|500|Internal server error|The server is confused; this may be caused by an error in the server-side program responding to the request.|
|501|Method not implemented|The request method used is invalid; this could be caused by a typing error, such as Get in place of GET.|
|502|Bad gateway|The proxy or gateway indicates that it received a bad response from the upstream server.|
|503|Service unavailable|The server cannot respond due to overloading or maintenance. The client can try again later.|
|504|Gateway timeout|The proxy or gateway indicates that it received a timeout from an upstream server.|
##  Data types
Now that we have looked at HTTP methods and return codes, let's look at the data that is sent or received during a GET or POST. Let's look at an example and see how the same information is represented in the various data types. The data sent and received in a RESTful connection requires structured data formatting. **Standard data formats include XML, JSON, and YAML**, which are described in the following sections.

### XML
Extensible Markup Language (XML) is a markup language that encodes information between descriptive tags. XML is a superset of Hypertext Markup Language (HTML), which was originally designed to describe the formatting of web pages served by servers through HTTP. The encoded information is defined within user-defined schemas that enable any data to be transmitted between systems. An entire XML document is stored as text, and it is both machine readable and human readable.
### JSON
JSON, short for JavaScript Object Notation, is pronounced like the name Jason. The JSON format is derived from JavaScript object syntax, but it is entirely text based. It is a key: value data format that is typically rendered in curly braces {} and square brackets []. JSON is readable and lightweight, and it is easy for humans to understand. A key/value pair has a colon (:) that separates the key from the value, and each such pair is separated by a comma in the document or the response.
JSON keys are valid strings. The value of a key is one of the following data types:

- String
- Number
- Object
- Array
- Boolean (true or false)
- Null
### YAML
YAML is an acronym that stands for YAML Ain't Markup Language. According to the official YAML site (https://yaml.org), "YAML is a human-friendly data serialization standard for all programming languages."

YAML is a data serialization language designed for human interaction. It's a strict superset of JSON, another data serialization language. But because it's a strict superset, it can do everything that JSON can do and more. One significant difference is that newlines and indentation mean something in YAML, whereas JSON uses brackets and braces to convey similar ideas. YAML uses three main data formats:

-Scalars: The simplest is a keyvalue view.
-Lists/sequences: Data can be ordered by indexes.
-Dictionary mappings: These are similar to scalars but can contain nested data, including other data types.

## Webhooks
**Webhooks are user-defined HTTP callbacks.** A webhook is triggered by an event, such as pushing code to a repository or typing a keyword in a chat window. An application implementing webhooks sends a POST message to a URL when a specific event happens. Webhooks are also referred to as reverse APIs, but perhaps more accurately, a webhook lets you skip the request step in the request/response cycle. No request is required for a webhook, and a webhook sends data when triggered.
For security reasons, the REST service may perform some validation to determine whether the receiver is valid. A simple validation handshake performs validation, but this is just one way of validating.

The validation token is a unique token specified by the server. Validation tokens can be generated or revoked on the server side through the configuration UI. When the server sends data to a webhook URL, it includes a validation token in the request HTTP header. The webhook URL should consist of the same validation token value in the HTTP response header. In this way, the server knows that it is sending to a validated endpoint and not a rogue endpoint.

You will face a particular difficulty when developing an application that consumes webhooks. When using a public service that provides webhooks, you need a publicly accessible URL to configure the webhook service. Typically, you develop on localhost, and the rest of the world has no access to your application, so how do you test your webhooks? ngrok (http://ngrok.com) is a free tool that allows you to tunnel from a public URL to your application running locally.

## Sequence Diagrams

Now that you understand the fundamentals of REST API (request, response, and webhooks), authentication, data exchange, and constraints that go with rest APIs, it's time to introduce sequence diagrams. A sequence diagram models the interactions between various objects in a single use case. It illustrates how the different parts of a system interact with each other to carry out a function and the order in which the interactions occur when a particular use case is executed. In simpler terms, a sequence diagram shows how different parts of a system work in a sequence to get something done.

The sequence of events that occur is as follows:

- The client browser points to http://myhouse.cisco.com/ (the HTTP GET request sent), which is the web application.
- The server sends out a REST API request to get all the rooms to the back-end service (/API/getallrooms) to get all the details of the house.
- The back-end API service returns data in JSON format.
- The web application processes the JSON and renders the data in the user interface.
- The client sees the data.

## REST Constraints
REST defines six architectural constraints that make any web service a truly RESTful API. These are constraints also known as Fielding's constraints (see https://www.ics.uci.edu/~fielding/pubs/dissertation/top.htm). They generalize the web's architectural principles and represent them as a framework of constraints or an architectural style. These are the REST constraints:

- **Client/server**: The client and server exist independently. They must have no dependency of any sort on each other. The only information needed is for the client to know the resource URIs on the server. The interaction between them is only in the form of requests initiated by the client and responses that the server sends to the client in response to requests. The client/server constraint encourages separation of concerns between the client and the server and allows them to evolve independently.
- **Stateless**: REST services have to be stateless. Each individual request contains all the information the server needs to perform the request and return a response, regardless of other requests made by the same API user. The server should not need any additional information from previous requests to fulfill the current request. The URI identifies the resource, and the body contains the state of the resource. A stateless service is easy to scale horizontally, allowing additional servers to be added or removed as necessary without worry about routing subsequent requests to the same server. The servers can be further load balanced as necessary.
- **Cache:** With REST services, response data must be implicitly or explicitly labeled as cacheable or non-cacheable. The service indicates the duration for which the response is valid. Caching helps improve performance on the client side and scalability on the server side. If the client has access to a valid cached response for a given request, it avoids repeating the same request. Instead, it uses its cached copy. This helps alleviate some of the server's work and thus contributes to scalability and performance.**Note**( **GET** requests should be cacheable by default. Usually browsers treat all GET requests as cacheable.,**POST** requests are not cacheable by default but can be made cacheable by adding either an Expires header or a Cache-Control header to the response.**PUT and DELETE** are not cacheable at all.)
- **Uniform interface:** The uniform interface is a contract for communication between a client and a server. It is achieved through four subconstraints:**Identification of resources:** As we saw earlier in the chapter, resources are uniquely identified by URIs. These identifiers are stable and do not change across interactions, even when the resource state changes. **Manipulation of resources through representations:** A client manipulates resources by sending new representations of the resource to the service. The server controls the resource representation and can accept or reject the new resource representation sent by the client. **Self-descriptive messages:** REST request and response messages contain all information needed for the service and the client to interpret the message and handle it appropriately. The messages are quite verbose and include the method, the protocol used, and the content type. This enables each message to be independent.**Hypermedia as the Engine of Application State (HATEOS):** Hypermedia connects resources to each other and describes their capabilities in machine-readable ways. Hypermedia refers to the hyperlinks, or simply links, that the server can include in the response. Hypermedia is a way for a server to tell a client what HTTP requests the client might want to make in the future.
- **Layered system:** A layered system further builds on the concept of client/server architecture. A layered system indicates that there can be more components than just the client and the server, and each system can have additional layers in it. These layers should be easy to add, remove, or change. Proxies, load balancers, and so on are examples of additional layers.
- **Code on demand:** Code on demand is an optional constraint that gives the client flexibility by allowing it to download code. The client can request code from the server, and then the response from the server will contain some code, usually in the form of a script, when the response is in HTML format. The client can then execute that code.

### REST API Versioning

Versioning is a crucial part of API design. It gives developers the ability to improve an API without breaking the client's applications when new updates are rolled out. Four strategies are commonly employed with API versioning:

- **URI path versioning:** In this strategy, the version number of the API is included in the URL path.
- **Query parameter versioning:** In this strategy, the version number is sent as a query parameter in the URL.
- **Custom headers:** REST APIs are versioned by providing custom headers with the version number included as an attribute. The main difference between this approach and the two previous ones is that it doesn't clutter the URI with versioning information.
- **Content negotiation:** This strategy allows you to version a single resource representation instead of versioning an entire API, which means it gives you more granular control over versioning. Another advantage of this approach is that it doesn't require you to implement URI routing rules, which are introduced by versioning through the URI path.

## REST Tools
