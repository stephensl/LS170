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
      - dependent on TCP at Transport Layer for reliable HTTP messages.
      - dependent on TLS if we wish to transfer messages securely. 
        - subject to inherent complexities and inefficiencies. 

    - Solution: 
      - QUIC Protocol
        - provides reliability and security features that have traditionally been provided by TCP/TLS combo. 
    
    

          
	


