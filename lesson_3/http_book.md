# Introductory HTTP 

## Overview
  - Browser is the interface or window through which you interact with world wide web. 
    - Under the hood, browser includes collection of files to properly display the page. 
      - Files may include CSS, HTML, Javascript, images, videos, etc. 
      - These files were sent from a **server** to your browser (**client**) by an application protocol called HTTP. 

  - HTTP 
    - Protocol that serves as a link between application and transfer of hypertext documents. 
      - Essentially an agreement or message format of how machines communicate with each other. 
    - Follows simple model: 
      - Client makes a request to a server and waits for a response. 
      - HTTP is a request-response protocol. 
      - Request and response follow standard format that other machine can interpret. 

  - Domain Name System (DNS)
    - When we type 'google.com' how does computer map to appropriate IP address for server?
      - Handled by Domain Name System
        - Distributed database
        - Keeps track of domain names and corresponding IP addresses on internet. 
      - DNS databases stored on computers called DNS servers.
        - No single server has complete database.
          - If server does not have requested domain name, routes request to another DNS server up hierarchy. 
  
  - Simplified Interaction with Internet using web-browser:
    - Enter URL like http://www.google.com into address bar.
    - Browser creates an HTTP request, packages it, and sends to device's network interface. 
    - If device already has record of IP address, it will use this cached address. 
      - If not, a DNS request will be made to Domain Name System to obtain IP address for domain. 
    - Packaged HTTP request goes over internet where it's directed to server with matching IP address. 
    - Remote server accepts request, and sends response over the internet back to network interface.
      - Network interface hands response to browser. 
    - Browser displays the response in form of web page. 

  - Key Points from simplified interaction steps:
    - When browser issues a request, it is simply sending some text to an IP address. 
    - Because the client (web browser) and server (recipient of request) have an agreement on protocol in form of HTTP, the server can take apart the request, understand its components, and send a response back to web browser. 
    - Web browser then processes the response strings into content that you can understand. 


### Clients and Servers
  - Most common client is application called a Web Browser.
    - Chrome, Safari, Firefox, etc.
    - Responsible for issuing HTTP requests and processing HTTP response into user-friendly format on screen. 
  - Many other tools and applications (clients) can issue HTTP requests as well. 

  - Content being requested is located on a remote computer called a server. 
    - Servers are devices capable of handling inbound requests. 
      - Job of server is to issue response back to client. 

### Resources
  - Generic term for items you interact with on the internet via a URL.
    - images
    - videos
    - web pages
    - other files
    - software
  - No limit to number of resources available over the internet. 

### Statelessness
  - Protocol is stateless if: 
    - designed in such a way that each request/response pair is completely independent of previous one. 
  - HTTP is stateless protocol
    - server does not need to keep track of information/state between requests. 
      - when request breaks in route to the server, no part of the system has to do any cleanup. 
    - Benefit is resilience
    - Tradeoff is difficulty in building stateful applications. 
      - Developers must work to simulate a stateful experience in web applications. 
  - The key concept to remember is that even though you may feel the application is stateful, underneath the hood, the web is built on HTTP, a stateless protocol. It's what makes the web so resilient, distributed, and hard to control. It's also what makes it so difficult to secure and build on top of.


## Uniform Resource Locator (URL)
  - Similar to an address or phone number needed in order to visit/communicate with a friend. 
  - Most frequently used part of the general concept of a Uniform Resource Identifier (URI) which specifies how resources are located.


  ### URL Components 
    - Example broken into 5 parts:
      
      - http://www.example.com:88/home?item=book 

        1. `http`: Scheme
          - always placed before colon and two forward slashes.
          - tells web client how to access the resource
          - in this case, tells web client to use HTTP to make a request. 

        2. `www.example.com`: Host 
          - tells the client where the resource is hosted or located. 

        3. `:88`: Port
          - Only required if you want to use a port other than the default.
          - default port number for HTTP is port 80. 

        4. `/home`: Path 
          - optional 
          - shows what local resource is being requested.
          - may point to specific resource on the host.

        5. `?item=book`: Query String
          - optional 
          - made up of query parameters
          - used to send data to the server 


### Query Strings and Parameters 
  - Usually only used with HTTP GET requests. 
    - whenever you type URL in address bar of web browser, issuing HTTP GET request. 
      - most links also issue HTTP GET requests, with some minor exceptions. 
  
  - A simple URL with a query string may look like:
    - http://www.example.com?search=ruby&results=10

      - `?` is a reserved character marking the start of the query string. 
      - `search=ruby` is a parameter name/value pair. 
      - `&` is a reserved character used when adding more parameters to query string. 
      - `results=10` is also a parameter name/value pair. 

  - Another example: 
    - http://www.phoneshop.com?product=iphone&size=32gb&color=white
      - name/value pairs include: 
        - `product=iphone`
        - `size=32gb` 
        - `color=white`
    - Asks the server to narrow down on a product. 
    - How the server uses these parameters is up to the server side application. 


  - Query Strings
    - Benefit: 
      - allow you to pass in additional information to the server. 
    - Limitations: 
      - maximum length
      - name/value pairs used in query strings are visible in the URL.
        - passing sensitive info like username/password to the server this way is not recommended. 
      - spaces and special characters like `&` cannot be used with query strings. They must be URL encoded. 

### URL Encoding
  - URLs only accept certain characters in the standard 128 character ASCII character set. 
    - Reserved or unsafe ASCII characters not being used for intended purpose, or characters not in the set must be encoded. 
  - Functions to replace non-conforming characters with `%` followed by two hexadecimal digits that represent the equivalent UTF-8 character. 
    - UTF-8 uses 1-4 bytes to represent every possible character in the Unicode character set. 
  - Examples: 
    - space -> %20
    - $ -> %24 

  ### Characters must be encoded if: 
    - They have no corresponding character within the standard ASCII character set. 
      - Note that this means all extended ASCII characters as well as 2-, 3-, and 4-byte UTF-8 characters. 
    - The use of the character is unsafe- meaning it may be misinterpreted or modified by some systems. 
      - % is unsafe, since its used to encode other characters. 
      - other unsafe characters include: 
        - spaces
        - quotation marks
        - `#` 
        - `<` `>`
        - `{` `}`
        - `[` `]`
        - `~` 
    - The character is reserved for special use in URL scheme. 
      - Presence in URL serves a specific purpose
        - `/`
        - `?`
        - `:`: host/port delimiter or user/password delimiter. 
        - `@`
        - `&`: string query delimiter
      
### Safe Characters for URLs
  - Alphanumeric 
  - Special characters
    - `$`
    - `-`
    - `_`
    - `+`
    - `!` 
    - `'`
    - `()`
    - `"`
    - `,`
  - Reserved characters being used for reserved purpose
    - otherwise must be encoded. 


## Making HTTP Requests 

### Chrome Tools 
  - Method column 
    - Information displayed here known as the HTTP Request Method
      - This is the verb that tells server what action to perform on a resource. 
        - GET and POST are most common. 
          - GET
            - Retrieving information
            - Most commonly used
  - Status column 
    - Every request gets a response (unless the request times out)
    - Response is given, even if response is error. 

### GET Requests
  - Initiated by clicking on link or via address bar of browser.
    - Default behavior of link is to issue GET request to a URL. 
  - GET requests are used to retrieve a resource. 
  - The response from a GET request can be anything, but if HTML and HTML references other resources...
    - Browser automatically requests those referenced resources
      - A pure HTTP tool will not. 

### POST Requests 
  - HTTP method used when...
    - want to initiate some action on the server
    - send data to a server 
  - Allows sending much larger and sensitive data to the server.
    - Images
    - Videos
  - Example: sending username/password to server for authentication
    - GET request and send through query string
      - Would expose sensitive info in URL.
    - Use POST request in a form. 
      - Does not have same size limitations of GET request query strings.

  **How are we sending data to the server since not through URL?**
    - Through the HTTP body
      - Body contains data being transmitted in an HTTP message
        - Optional
        - May send HTTP messages with empty body
      - Body can contain HTML, images, audio, etc. 
        - Body is like the letter, enclosed in an envelope, to be posted. 
    
    - The POST request  is the same as...
      - Filling out form in browser
      - Submitting form
      - Being redirected to next page
        - How to know where?
          - Included in Location HTTP response header from server.
            - Browser sees Location header and automatically issues new, unrelated request to the specified URL

  **Key Points**
    - Browser hides a lot of underlying HTTP request/response cycle
      - Browser initiated the initial POST request
      - Browser received response with Location header
        - Issued another request without action from user
        - Displayed response from second request. 
      - Pure HTTP tool does not issue next request automatically, while browser does. 

    

### HTTP Headers 
  - Allow client and server to send additional information during HTTP Request/Response cycle. 
  - Syntactically written as colon-separated name:value pairs in plain text. 

#### Request Headers 
  - Give more information about client and resource to be fetched.
  - Part of request sent to server.
    - Host
      - Domain name of the server
        - Ex. Host:www.reddit.com 
    - Accept-Language 
      - List of acceptable languages 
        - Ex. Accept-Language:en-US,en;q=0.8
    - User-Agent
      - String that identifies the client
        - ex. User-Agent:Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/112.0.0.0 Safari/537.36
    - Connection 
      - Type of connection the client would prefer.
        - Ex. Connection:keep-alive
        
### Most important components of HTTP request: Method, Path, Header, Body (MPHB)
  - Method
    - Indicates desired action to be performed on the specified resource.
    - Most common
      - GET (retrieve a resource)
      - POST (send data to server)
    - Others
      - DELETE (delete a resource)
      - HEAD (retrieve resource metadata)
  
  - Path 
    - resource name and any query parameters
      - Specific URL being requested 
      - Any query parameters as additional data appended to URL

  - Header
    - Provide additional context or information about the request or the client. 

  - Body 
    - For POST requests
      - The data being sent to the server.



## Processing Responses
  - Raw data returned by the server is the *response*.

### Status Code
  - Three digit number that server sends back after receiving a request
    - Signifies status of request
  - Common Status Codes
    - 200 
      - OK
      - Request handled successfully
    - 302
      - Found 
      - The requested resource has changed temporarily
        - Usually results in redirect to another URL
    - 404 
      - Not Found
      - Requested resource could not be found.
    - 500
      - Internal Server Error
      - The server encountered a generic error


  #### 302 Found
    - When resource is moved...
      - Most common strategy is to *redirect*, re-routing request to new URL.
      - When browser sees response status code 302...
        - knows resource has been moved
        - automatically follow new re-routed URL in `Location` response header.

    ##### Redirect workflow example:
      - Visiting github.com/settings/profile 
        - In order to access profile, must first be signed in
          - If not signed in, browser directs you to a page to do so.
        - After credentials entered, redirected to original page trying to access.

        

