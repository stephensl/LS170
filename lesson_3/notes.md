# Intro to HTTP 

## Focus Areas
  - Develop clear understanding of role of HTTP 
    - Build mental model of web as combination of multiple technologies.
      - HTTP plays specific role in the combination working together.
  - Breaking things down into individual components
    - Ensure clarity by breaking down concepts like HTTP and URL into specific components.
      - Spend time examining and understanding the purpose of each component. 
  

## The Application Layer 
  
  - Top layer in TCP/IP and OSI model
    - OSI emphasis on different functions or services at each layer defines two other layers:
      - Between Transport and Application Layer
        - Session Layer
        - Presentation Layer
    - The protocols existing at Application Layer most directly interact with application. 
  
  - Not application itself
    - Set of protocols which provide communication services to applications. 
  
  - Networked applications are not limited to interacting with only Application Layer
    - May interact with Transport Layer protocols by opening a TCP socket.
    - Much less common for applications to interact directly with layers below Transport. 
  
**Application Layer protocols rely on the protocols at the layers below to ensure that a message gets to where it needs to go, and instead focuses on the structure of the message and data it should contain.** 


### Application Layer Protocols 
  - Rules for how applications talk with each other at a syntactical level. 
    - Different types of applications have different requirements.
      - Many different protocols at Application Layer. 
        - Examples: 
          - Rules for how an email client communicates with an email server are different than rules for how a web browser communicates with a web server.
          - If application for transferring files: 
            - likely use FTP
          - If email client: 
            - SMTP
            - POP
            - IMAP

**HTTP is primary protocol used for communication on the web.**


### Web vs Internet 
  - Internet
    - Network of networks
    - Infrastructure that enables inter-network communication
      - physical network and lower-level protocols that control its use. 
  - Web 
    - Service that can be accessed via the internet. 
    - Vast information system comprised of resources navigable by means of a URL (Uniform Resource Locator).
    - HTTP is the primary means by which applications interact with the resources that make up the web. 
  

### Web History
  - Problem: 
    - Lots of information distributed across many different computers. 
    - Although computers connected over network, information stored on them was difficult to access. 
  - Solution: 
    - Use internet connectivity and Hypertext to create accessible information system. 
    - Information exists on various computers as structured resources. 
      - Resources connected using hyperlinks. 
  - Needs: 
    - Uniformity
      - structure of resources for rendering/viewing
      - resource addressing for simple locating
      - requests for resources and response to request. 
  - Protocols providing uniformity: 
    - Combination of 3 technologies or concepts: 
      - HTML (Hypertext Markup Language)
      - URI (Uniform Resource Identifier)
      - HTTP (Hypertext Transfer Protocol)

  ### Hypertext Markup Language (HTML)
    - Means by which resources in system should be uniformly structured. 
      - Early version intended for structuring text documents.
        - Included only 18 elements. 
        - Most revolutionary was anchor element `<A>` which uses a `href` attribute to provide link from one resource to another.

  ### Uniform Resource Identifier (URI)
    - System by which resources should be uniformly addressed on the web. 
    - Distinct points in the information space that is the web.
    - Often used interchangeably with URL- differences to be discussed later. 


  ### Hypertext Transfer Protocol (HTTP)
    - Set of rules providing uniformity to how resources on web are transferred between applications. 
      
      
      - (Intro to HTTP Book notes in separate file)






## Background/Diagrams 
  - Mental model of where you are at higher level when looking at piece of code. 

### Client-Server Paradigm 
  - HTTP
    - Stateless protocol for how clients communicate with servers.
    - Simply: 
      - client issues HTTP request to server.
      - server processes the request.
      - server sends response back to client.

#### Zooming in on Server 
  - The server side infrastructure in entirety is the "server" to the client.
    - Server may be distributed across numerous machines. 
      - May include many intermediary machines, load balancers, etc. 
    
  ##### 3 Primary Server-side infrastructure elements
    
    - Web Server
      - responds to request for static assets
        - files 
        - images
        - CSS, JavaScript, etc.
      - requests do not require data processing, so handled by simple web server.

    - Application Server
      - application or business logic 
        - handling more complex requests
      - server-side code lives here
      - often consults persistent data store to retrieve or create data

    - Data Store
      - persistent data storage
        - relational database
        - simple files
        - key/value stores
      - primary role is saving data in some format for later retrieval and processing.
      - data persists between stateless request/response cycles.


#### HTTP over TCP/IP
  - HTTP relies on TCP/IP connection most of the time. 
    - HTTP operates at application layer
      - concerned with structuring messages exchanged between applications.
    - TCP/IP ensures that the request/response cycle gets completed between browser/server.



## URLs
  - URLs are the most frequently used part of the general concept of a Uniform Resource Identifier (URI)
    - URI (generic identifier)
      - sequence of characters that identifies an abstract or physical resource
      - all URLs are URIs but not vice versa.
    - URL (implementation of URI)
      - subset of URIs that in addition to identifying a resource:
        - provides means of locating resource by describing primary access mechanism (network location)

  ### Schemes and Protocols 
    - Scheme
      - prepends `://` 
      - identifies which family of protocols should be used to access the resource.
        - Not specific protocol (HTTP vs HTTP 1.1)
      - in general URI context
        - scheme is specification for assigning identifiers within that scheme.
          - not related to particular protocol
          - lowercase is convention

  ### URLs and Filepaths 
    - Initially intention of web was to provide access to content of static HTML files.
      - path portion of the uURL represented a physical file location on the Web server.
    
    - Today, much of content is generated dynamically
      - may take place on server or client side
        - Server Side: framework or applications combine templates with stored data to produce HTML pages which form the body of an HTTP response. 
        - Client Side: framework where HTTP response contains the raw data which is then manipulated by an application running in the browser before being rendered. 
      
      - Way in which the path portion of the URL is used is determined by application logic 
        - may not bear any relationship to underlying file structure on server. 
        - often involves URL pattern matching to match path to pre-defined route that executes some specific logic. 
    


## Practice Problems: URL Components

  1. Given this URL: 
  `https://amazon.com/Double-Stainless-Commercial-Refrigerator/B60HON32?ie=UTF8&qid=142952676&sr=93&keywords=commercial+fridge`

    - host: 
      - `amazon.com` 

    - names of query parameters: 
      - `ie`
      - `qid`
      - `sr` 
      - `keywords`

    - values of query parameters:
      - `UTF8`
      - `142952676`
      - `93`
      - `commercial + fridge` 

    - scheme: 
      - `https`

    - path: 
      - `/Double-Stainless-Commercial-Refrigerator/B60HON32`

    - port: 
      - does not contain port
      - most will use port 443 due to having scheme of `https`
        - not included within the URL


  2. Add the port 3000 to the following URL:
    `http://amazon.com/products/B60HON32?qid=142952676&sr=93`

  
    -  `http://amazon.com:3000/products/B60HON32?qid=142952676&sr=93`


  3. Given URL: `http://localhost:4567/todos/15`

    - query parameters: 
      - none

    - scheme: 
      - `http` 

    - path: 
      - `/todos/15`

    - host: 
      - `localhost`

    - port: 
      - `:4567` 


  4. What are two different ways to encode a space in a query parameter?
    - `%20`
    - `+`

  5. What character indicates the beginning of a URL's query parameters?
    - `?`

  6. What character is used between the name and value of a query parameter?
    - `=`

  7. What character is used between multiple query parameters?
    - `&`

  

### Request Response Cycle Video
  - Practice Questions: 

    1. What are required components of an HTTP request? 
      - Method: GET, POST, etc.
      - Host header
      - HTTP version
      - Path: where to locate resource 
        - technically path is called the "request URI" 

    2. What are some optional components of HTTP request?
      - Query parameters
      - Body
      - Additional headers 

    3. What are the required components of an HTTP response? 
      - Status line with status code
    
    4. What are the additional optional components?
      - Headers
      - body 

    5. What determines whether a request should use GET or POST as its HTTP method?
      
      - Client
        
        - Are we asking for data from the server? (GET)
          - "read only" operations
            - subtle exceptions: webpage view tracking uses GET since main content of page doesn't change.
        
        - Are we providing data to the server? (POST)
          - changing values stored on the server.
            - most HTML forms that submit their values to the server use `POST`. 
              - exception is search forms: often use `GET` as not changing data on server, just viewing it. 


## Lesson 3 Summary
  - Domain Name System (DNS)
    - distributed database
    - maps domain name to IP address

  - URI (Uniform Resource Identifier)
    - generic identifier for particular resource in information space

  - URL (Uniform Resource Locator)
    - subset of URI
    - particular rules/components make it a URL 
      - include scheme, host, port, path, and query string.

  - Query Strings
    - used to pass additional information to server during HTTP request.
    - name=value pairs 
      - multiple pairs delimited by `&`
    - `?` signifies start of query string

  - URL Encoding
    - certain characters in URL are replaced with ASCII code.
      - used if: 
        - character has no corresponding character in the ASCII set
        - character unsafe because used for encoding other characters
        - character reserved for special use within URL

  - HTTP Message Exchange
    - includes Request and Response
    - generally between client and server
    - client sends request; server sends response

  - HTTP Request Contents
    - request line
    - headers
    - optional body

  - HTTP Response Contents
    - status line (includes status code)
    - optional headers
    - optional body 

  - Statelessness
    - HTTP is stateless protocol 
      - Each request/response cycle is independent of previous or subsequent.
    
    - Statefulness simulated through techniques: 
      - session IDs
      - cookies
      - AJAX 

  - HTTP Insecure 
    - Increase security by using `HTTPS` 
      - enforcing Same-origin policy 
      - preventing Session Hijacking 
      - preventing Cross Site Scripting 