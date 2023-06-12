# Evolution of Network Technologies

## Focus Areas
  - Awareness level content for additional background/context in evolution of network tech.
  
  - How and Why HTTP is evolving
    - History of HTTP and changes over time
      - helps understand workarounds used to deal with limitations. 
      - changes are in response to limitations or problem solving
  
  - Functionality provided through browser APIs
    - modern browsers provide numerous APIs that provide functionality that HTTP cannot alone. 
    - awareness of different APIs and service they offer

  - Client-Server is NOT the only network paradigm
    - although very prevalent on the web, not the only paradigm
    - awareness of other network paradigms 
      - helpful when making high level design decisions about networked apps


## HTTP: Past, Present, Future
  ***HTTP is an evolving protocol***

  ### HTTP/0.9 (1991 release)
    - Characterized by *simplicity*. 
      - "the one line protocol"
    - Request
      - single line
      - no headers or request body
      - consisted of the method `GET` and the path to resource on server.
        - instead of URI/URL (connection already would have been established)
    - Response 
      - single hypertext document 
        - no headers or other meta data 
        - no status codes or version numbers
      - end of response signaled by server closing the connection.


  ### HTTP/1.0 
  - 1991-1996 events leading to mass adoption of internet.
    - Netscape Navigator 1.0: first commercial browser
    - Telecom companies provide internet access via dial up
      - Used existing telephone network (bandwidth apron 56 kbps)
    - World Wide Web Consortium (W3C) and HTTP Working Group (HTTP-WG)
	    - formed and provided framework for documentation/standardization
    
    - Numerous improvements to HTTP between '91-'96
	    - HTTP/1.0 attempt to document set of practices and usage patterns.
	    - Documented in RFC1945
    
    - Improvements to Protocol
      - Request
        - Addition of two HTTP methods `HEAD` and `POST`.
        - Request line more flexible and varied
        - Request URI portion could be path or absolute URI
        - HTTP version added to end of request line for server interpretation
      - Response
        - Status line, comprised of status code with text status and HTTP version
        - HTTP Headers
          - Key/value pairs provided additional info to deal with growing complexity of requests and responses. 
    
***Developments often in response to other developments or the changing internet ecosystem.***

  ### HTTP/1.1
  - First standard version of HTTP
    - Initially released in 1997, then updated in 1999 as RFC2616.
  
  - Improvements: 
    - Generally addressed interoperability issues and performance improvements for the type of content now being produced for the web. 

  - Connection Improvement
    - Problem: 
      - HTTP/1.0 still operated on the basis of using a separate TCP connection for each request-response cycle. 
        - Client opens connection to server and makes request.
        - Server provide response and close the connection. 
          - If client needed to make another request, it would open a new connection.
        - As web grew, complexity increased: 
          - embedded images
          - CSS style sheets (1996)
          - JS scripts (1995)
        - All these resources needed to be fetched using separate HTTP request. 

    - Major Advancements of HTTP/1.1
      - **Connection Reuse** 
        - same TCP connection used for making multiple requests. 
          - reduced overhead in latency required for TCP handshake
          - allowed for **pipelining** of requests.
            - client does not need to wait for response before sending more requests. 
        - Cache control mechanisms
        - More HTTP methods
          - `PUT`
          - `DELETE`
          - `TRACE`
          - `OPTIONS`
        

### HTTP/2 (2015)
  - Increased complexity and emphasis on visual data and embedded files along with level of interactivity requires many more HTTP requests to be made. 
    - May take dozens of HTTP requests to render a single webpage and provide its functionality. 
  
  - Performance Optimization
    - Pipelining allows for multiple requests to be sent at once (reducing latency), but efficiency limitations exist. 
      - Limitations:
        - Server must respond in order they are sent
          - May cause Head of Line blocking.
      
    - Solution: 
      - **Metaplexing** instead of pipelining. 
        - Multiple requests can still be sent at same time, but in parallel instead of relying on message order. 
      - Compression of headers
        - reducing size, as headers can often make up large part of request or response. 
      
  
  ### HTTP/3
    - HTTP/2 has not been fully adopted
    - Problem: 
      - Primarily network congestion and latency.
      - dependent on TCP at Transport Layer for reliable HTTP messages.
      - dependent on TLS if we wish to transfer messages securely. 
        - subject to inherent complexities and inefficiencies. 

    #### Comparison

| Feature | HTTP/1.x | HTTP/2 | HTTP/3 |
|---------|----------|--------|--------|
| Multiplexing | No | Yes | Yes |
| Header Compression | No | Yes (HPACK) | Yes (QPACK) |
| Transport Protocol | TCP | TCP | QUIC (over UDP) |
| Server Push | No | Yes | Yes |
| Prioritization | No | Yes | Yes |
| Binary or Textual | Textual | Binary | Binary |
| Stream Dependencies | No | Yes | Yes |

  - Server Push
    - when the server responds to the initial request, it can also "push" the additional resources to the client's cache before the client requests them. This can significantly improve the performance of a website by reducing the number of round trips needed to fetch all the necessary resources.

  - Prioritization: 
    - This is a feature in HTTP/2 and HTTP/3 that allows the client to specify the importance of multiple requests. This means that the client can tell the server which resources it needs first. For example, it might want to load critical CSS and HTML before loading images. This can significantly improve the perceived performance of a website, as users can start interacting with the page while less important resources are still loading.

  - Binary vs Textual: 
      - This refers to the format in which data is sent over the network. In HTTP/1.x, data is sent as text, which is easy to read and debug but not very efficient. In HTTP/2 and HTTP/3, data is sent in a binary format, which is more compact and efficient, leading to faster transmission times. However, binary data is not human-readable, which can make debugging more challenging.

  - Stream Dependencies: 
      - This is another feature in HTTP/2 and HTTP/3 that allows the client to express relationships between multiple requests. For example, the client might specify that certain requests depend on the responses to other requests. This allows the server to better understand the client's needs and optimize the order in which it processes and responds to requests. Like prioritization, stream dependencies can improve the perceived performance of a website by ensuring that the most important resources are loaded first.

    - Solution: 
      - QUIC Protocol (Quick UDP Internet Connections)
        - built on top of UDP
        - provides reliability and security features that have traditionally been provided by TCP/TLS combo. 
    
    **Most significant difference from prior versions is use of QUIC as transport protocol.**

    - Benefits 
      - Reduced latency
        - QUIC establishes connections faster than TCP
          - avoids Head of Line Blocking 
      - Improved security 
        - QUIC includes built in encryption
      - Greater efficiency 
        - QPACK header compression more efficient that HTTP/2's HPACK, reducing data size.
      - Forward Error Correction
        - allows receiver to correct errors without needed a retransmission from sender.
      - Combines the reliability of TCP with the speed of UDP. It also includes built-in encryption, providing a level of security comparable to TLS. This integrated approach to reliability and security simplifies the networking stack and can lead to better performance.
      
    - Tradeoffs/Limitations
      - UDP blocking
        - some networks block UDP traffic
      - CPU usage 
        - QUIC encryption and decryption in user space can lead to higher CPU usage
      - Network support
        - As a new protocol, no all networks/server support it yet.

   
  
## Web Performance and HTTP Optimizations
  **With increased complexity of data on the web, performance and optimization are impacted.**
  - Request is made to retrieve web page in the browser
    - Browser will receive document structure and begin loading. 
      - As browser loads the web page structure...
        - hypermedia resources defined in the page are requested via a new TCP connection
          - every TCP connection starts with round trip handshake: increased latency. 
            - connection re-use was major advancement in HTTP/1.1
  - With modern web applications, we have a complex dependency graph created with each load as the application needs to build the basic structure of the content, render the stylesheets used to define the layout, fetch all the needed resources, and run the scripts used to respond to user interaction.


  ### Browser Optimizations
    - Two broad types: 
      
      - Document Aware Optimizations
        - when browser can identify and prioritize fetching resources
          - goal: to more efficiently load webpage
          - method: prioritize certain resources such as CSS layouts, and JS which can take the longest to load. 

      - Speculative Optimizations
        - when browser learns navigation patterns of user over time and attempts to predict user actions.
          - may involve: 
            - pre-resolving DNS names
            - pre-rendering frequently visited pages
            - opening TCP connection in anticipation of HTTP request when user hovers over link
  

  ### Latency as main limiter
    - major performance limiter for any software that relies on network connection. 
      - there will always be a certain level of latency due to physical distance
    - developers must optimize to reduce latency
      - eliminating unnecessary round trips 
      - minimizing resources to be fetched 
      - adding components to our system

    #### Further Optimizations 
     
      - Reducing resources/dependencies 
        - since every image, video, stylesheet, script can add to total number of requests, TCP connections, and latency overhead...
          - one of the most effective optimizations is to limit number of resources needing to be fetched. 
        - Example: JS file only used by one page but included on every page
          - browser requests file whether or not it actually hits the page. 
          - reducing page bloat and limiting resource need can improve performance. 
      
      - Compression
        - reduces size rather than number of resources to be fetched. 
        - smaller file size means less data and more efficient transfer.
        - Examples: 
          - using `gzip` on text based assets such as HTML, CSS, JavaScript
            - can reduce data size by 60-80
          - minification
            - removing unnecessary or redundant data
              - white space, code comments, formatting, shorter variable names, etc. 

      - Reusing TCP Connections
        - using same TCP connection to fetch multiple resources
          - "keepalive" connections (standard behavior in HTTP/1.1)


      - DNS Optimizations 
        - every initial request involves DNS lookup to map domain name of application to IP address of host server.
          - browser performs initial DNS lookup as well as those required for dependencies
            - until lookup complete, browser cannot connect to server or download any resources
        - Potential Solutions
          - Reducing number of host names to be resolved.
            - check if all included dependencies such as fonts or ext libraries are required for particular page view.
          - Download any external resources and host locally on server that is hosting web app
            - eliminates DNS lookups for those resources since under same hostname as application
          - Browser cache may already have library saved, so no need to fetch.

      - Caching 
        - server-side caching
          - short term memory bank
          - stores content recently requested by user so next time can be delivered more quickly.
            - useful in case of content that is dynamically generated by the server.
              - content that requires some sort of application logic to run in order to be produced
                - in contrast to static HTML files
        - performance benefits
          - reduces requests to be made to application server, by storing resources in cache
          - helps reduce load on application server
        - Implementation
          - no a trivial solution
          - must consider: 
            - which data to store in cache
            - when to remove data to free cache storage 
            - what data to invalidate



### Browser Networking APIs

  #### HTTP and Real-Time Data Synchronization
  - Not suited to real-time data sync
    - Example: liked facebook post updated number, notification without refreshing page.
  - Request/Response cycle not suited because requires a request to be sent by client before response.
    - modern web browsers provide several APIs that can be leveraged to assist this functionality. 
    
  - APIs

    - XHR
      - enables clients to manage requests and responses programmatically and asynchronously
        - web app can perform other actions while waiting for an update from the server
      - key component of AJAX (Asynchronous JavaScript and XML)
        - AJAX 
          - write JS to respond to user action
            - in response we can fetch some data from server and update part of page through DOM manipulation.
              - much faster than original behavior: shown in predictive search bar using google
      
      - Problem: 
        - in early days of web, nearly all links caused browser to send new request to the server.
          - upon receiving response, browser almost always had to completely load a new page, even if unchanged.
      
        - Solutions:
          - XHR allows web pages to send request to server then use response to alter just small part of page in the browser.
            - made web interactive/responsive
            - *polling*
              - could write script that runs in background of app and issues request to server periodically to check for updates
              - limitation of polling is may be unnecessary checks
                - *long-polling* server keeps connection idle until update available, then issues response.

          - Limitations: 
            - may not be best performance when compared to other tools
            - optimized for HTTP request/responses
              - does not support one side streaming messages to the other. 
            
      
      - SSE (Server-Sent Events)
        - Networking API enables efficient server to client streaming of text-based event data.
          - enables server to send real-time notification sor updates created by server to the client without requiring request to be sent by client. 

        - Implementation: 
          - Delivery of messages over single long-lives TCP connection. 
            - One client/server complete TCP handshake and first RR cycle...
              - instead of closing connection, client keeps it open to server to receive future updates 
              - messages can be pushed to client moment available on server
            - Benefit: 
              - low latency and minimum message overhead. 

          - SSE tradeoffs: 
            - only works with client/server model
            - does not allow for request streaming such as when streaming a large upload to the server
            - streaming support specifically designed to transfer UTF-8 data, meaning binary streaming inefficient. 

          - SSE Summary
            - offers efficient, low latency server to client streaming of text based data
              - client initiates connection adn server streams updates to client. 
              - after initial handshake, client can not send any data to server over that connection
                - only used for server to provide real time data updates to client

        
        - WebSocket 
          - enables bidirectional communication.
            - simple/minimal API enables persistent TCP connection that allows either side to independently send messages to each other. 
          - consists of messages and application code that does not need to worry about buffering, parsing, and reconstructing received data. 
          - provides low latency delivery of text and binary application data in both directions and good for delivering custom application protocols in the browser.

          - Limitations: 
            - Application must account for: 
              - state management
              - compression
              - caching 
              - other services provided by the browser
            - Not meant to be a replacement for HTTP, XHR, or SSE


### Peer to Peer Networking (P2P)
  - Alternative to client/server model.
    - Each computer within the network acts as a 'node'
      - nodes capable of performing both client and server functions as seen in client/server model.
    - **It's important to note that when we talk about a P2P network architecture, what this refers to is the way in which the various devices in that architecture interact with each other. The underlying infrastructure is the same as for a client-server architecture, including many of the protocols; for example, P2P networks can and do use TCP or UDP at the Transport layer.**

  
  - Use Cases
    - File sharing applications
      - no need to set up an maintain server to provide system with functionality: only need two or more nodes. 
      - lack of reliance on central server improves network resilience
        - several nodes may perform the same function, if one goes down, can still operate. 
    - Voice/Video calling 
      - no central routing point
        - may reduce latency by offering shorter paths between client and server.
        - useful in applications depending on real time communication.

  
  - Complexities
    
    - Main problem: 
      - Difficulty in discovery of other nodes on the network. 
        - with client/server model: 
          - assume server is available
          - has fixed/discoverable IP address 
        - with P2P
          - specific nodes may not always have same IP address
          - may be online or offline at various times.
      
      - Solutions: 
        - Depends on the type of P2P network being established: 
          
          - *flooding*: 
            - message is sent out to the network and each node forwards it until a specified number of network hops elapse.
              - any node capable of responding to the message does so. 
          
          - Distributed Hash Table (DHT)
            - table of key/value pairs 
              - ex. key is particular filename, value is id of network node which has file.
              - table split as to logically map underlying structure of nodes in the network
                - responsibility to maintain different parts of table distributed among different nodes.
          
          - Hybrid Model
            - central server that enables nodes to discover each other
            - nodes have client/server relationship with central server, but P2P with other nodes once connected. 
      
    - Additional complexities: 
      - connection negotiation and establishment
      - security
      - performance 
      - scaling


  #### WebRTC 
    - provides real-time communication functionality within the browser
      - allows browser to act as a node within a P2P communication network.
    - WebRTC  
      - collection of standards, protocols, and APIs available in most modern web browsers.
        - abstracts away complexities of establishing P2P communication between nodes.
      - uses UDP at Transport Layer
        - since UDP connectionless and unreliable...
          - combines various different protocols for session establishment and maintenance (STUN, TURN, ICE), for security (DTLS), and for congestion and flow control and a certain level of reliability (SRTP, SCTP).
      


      
## Summary 
  - HTTP has changed considerably over years, and continues to evolve. 
    - Many changes focused on improving performance in response to increasing demands of networked applications. 
  
  - Latency has big impact on performance of networked applications. 
    - Developers must be able to identify impact and mitigate through thoughtful optimizations.

  - Tools and techniques available to work around limitations of basic HTTP request response functionality. 

  - P2P may be more appropriate than Client-Server architecture for some use cases. 
