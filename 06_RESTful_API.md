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



## REST Constraints
## REST Tools
