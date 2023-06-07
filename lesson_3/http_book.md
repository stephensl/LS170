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
      - HTTP tool does not automatically follow the redirect.
        - If we look at Location in response header using HTTP tool
          - Same address as in address bar when redirected in browser.
      
  #### 404 Not Found 
    - Returned by server when the requested resource cannot be found. 
      - Browser will likely show default 404 page from site. 
      - HTTP tool will show raw response with the status code.
    
  #### 500 Internal Server Error 
    - Problem on the server side
      - Can be shown in variety of ways, similar to 404 page. 



### Response Headers 
  - Offer additional meta-information about response being sent back to client. 
    - Content-Encoding: 
      - type of encoding used on the data
        - Content-Encoding:gzip 
    - Server:
      - name of the server 
        - Server:thin 1.5.0 codename Knife 
    - Location: 
      - notify client of new resource location 
        - Location:https://github.com/login
    - Content-Type
      - contains the type of data contained in the response 
        - Content-Type:text/html;charset=UTF-8

  - Response headers have subtle effects on:
    - Data being returned
    - Workflow 
      - Ex. browser automatically following a `Location` in response header. 


### Summary Key Points 
  - HTTP is an agreement in the form of formatted text.
    - Dictates how a client and server communicate. 
  - Most important parts of HTTP response:
    - Status codes (200, 302, 404, 500)
    - Headers 
      - Contains additional meta-data regarding response.
    - Message body
      - Contains raw response data




## Stateful Web Applications 
  - HTTP is stateless
    - Server does not store information between each request/response cycle.
    - Each request made to a resources is treated as new entity.
    - Different requests are not aware of each other. 
  - Benefits of statelessness
    - Distributed
    - Resistant to control 
  - Limitations
    - Difficulty in building stateful web applications

### Stateful appearance
  - When we log into twitter...
    - see username at top, signifying authenticated status
    - click around, which generates new requests to twitter's servers
      - we are not suddenly logged out
      - the server response contains HTML that shows our username
      - application seems to maintain its state
  - How is this accomplished if HTTP is stateless?
    - Sessions
    - Cookies 
    - Asynchronous JavaScript calls, or AJAX
    - 4th approach no longer used:
      - sending stateful data as query parameters when making request


  ### A Stateful App
    - Twitter homepage
    - Login 
    - Notice username at top, showing authenticated status
    - Refresh page
    - Still logged in
  - How does the server know to remember my username and dynamically display it on the page even after sending new request?
    - HTTP protocol is being augmented to maintain a sense of statefulness. 
    - With help from client (browser) HTTP can be made to act as if it were maintaining stateful connection with server.

### How is this accomplished?
  
  #### Sessions
  - Having the server send some form of unique token to the client.
    - Whenever client makes a request to the server, client appends this token as part of request.
      - Allows for server to identify clients
  - Session Identifier: 
    - unique token that is passed back and forth
    - passing `session id` between client and server creates sense of persistent connection between requests.
      - each request, however, is technically stateless and unaware of the previous or next one.
  
    ##### Consequences 
      - Each request must be inspected to see if contains session identifier
        - If so, server must check to ensure session id is still valid
          - server must maintain some rules regarding session expiration and session data storage
      - Server must retrieve the session data based on the session id
      - Server must recreate the application state (HTML for a web request) from the session data
        - Send back to client as the response

      **server must work very hard to simulate stateful experience**

  #### Cookies 
    - One common way to store session information
    - Piece of data sent from server and stored in client during request/response cycle.
      - Small files stored in the browser and contain the session information.
  
  ##### How Cookies work
      - When visiting website for first time...
        - server sends session information and sets it in browser cookie on local computer.
        - actual session data is stored on the server
      - On each request...
        - client side cookie compared with server-side session data to identify current session.
        - when visit same webpage again, session will be recognized because of stored cookie with its associated information.
      - With session id sent with every request, server can now uniquely identify this client.
        - when server receives request with session id
          - server looks for associated data based on that id
          - in the associated session data is where server "remembers" state for that session id. 

  **Key Point on Cookies**
    - `session id` stored on client
      - used as a key to session data stored on server side
    - `session id` is unique and expires in relatively short time
      - required to login again after session expires
      - `session id` is deleted upon logout
    - To summarize: 
      - session data is generated and stored on the server-side
      - `session id` is sent to the client in form of a cookie
      - client uses session id as part of request as key for server to access session data. 


  ### Asynchronous JavaScript and XML (AJAX)
    - Allows browsers to issue requests and process responses *without a full page refresh*.
    - When AJAX is used, all requests sent from client are performed asynchronously
      - Page does not refresh.
    - Utilizes `callbacks` 
      - piece of logic passed on to a function to be executed after a certain event has happened.
  - KEY POINTS ABOUT AJAX
    - just like normal requests
      - sent to server with all normal components of an HTTP request, and server handles them like any other request.
        - Difference is that instead of browser refreshing and processing the response...
          - response is processed by a callback function, usually client-side JavaScript code. 
    

    

    
## Security 
  - HTTP is difficult to control, but also difficult to secure.
    - stealing session id
    - looking at cookies
    - etc

  - Secure HTTP (HTTPS)
    - client and server send requests/responses as strings
      - if attacker was attached to same network, could use *packet sniffing* techniques to read messages.
      - requests contain session id, so if copied, could craft request to server and pose as my client and be automatically logged in without needing to even access username and password. 
    - HTTPS
      - every request/response is encrypted before being transported on the network. 
      - uses cryptographic protocol called TLS (Transport Layer Security)
        - earlier versions of HTTPS used SSL (Secure Sockets Layer)
      - cryptographic protocols use certificates to communicate with remote servers and exchange security keys before encryption happens. 
  
  - Same Origin Policy 
    - permits unrestricted interaction between resources originating from the same origin
      - Origin refers to combination of scheme, host, and port.
    - restricts certain interactions between resources originating from different origins. 
  - Cross-origin Resource Sharing (CORS)
    - mechanism allowing for interactions that would normally be restricted cross-origin to take place.
      - Works by adding new HTTP headers, that allow servers to serve resources cross-origin to certain specified origins.

  - Session Hijacking 
    - if an attacker gets a hold of the session id, both the attacker and the user now share the same session and both can access the web application. In session hijacking, the user won't even know an attacker is accessing his or her session without ever even knowing the username or password.

  **Countermeasures for Session Hijacking**

    - One popular way of solving session hijacking is by resetting sessions. With authentication systems, this means a successful login must render an old session id invalid and create a new one. With this in place, on the next request, the victim will be required to authenticate. At this point, the altered session id will change, and the attacker will not be able to have access. Most websites implement this technique by making sure users authenticate when entering any potentially sensitive area, such as charging a credit card or deleting the account.

    - Another useful solution is setting an expiration time on sessions. Sessions that do not expire give an attacker an infinite amount of time to pose as the real user. Expiring sessions after, say 30 minutes, gives the attacker a far narrower window to access the app.

    - Finally, as we have already covered, another approach is to use HTTPS across the entire app to minimize the chance that an attacker can get to the session id.


  - Cross Site Scripting (XSS)
    - This type of attack happens when you allow users to input HTML or JavaScript that ends up being displayed by the site directly.
    - If the server side code doesn't do any sanitization of input, the user input will be injected into the page contents, and the browser will interpret the HTML and JavaScript and execute it. 
    - Example:
      - an attacker can use JavaScript to grab the session id of every future visitor of this site and then come back and assume their identity. It could happen silently without the victims ever knowing about it. Note that the malicious code would bypass the same-origin policy because the code lives on the site.

  - Potential solutions for cross-site scripting

    - One way to prevent this kind of attack is by making sure to always sanitize user input. This is done by eliminating problematic input, such as <script> tags, or by disallowing HTML and JavaScript input altogether.

    - The second way to guard against XSS is to escape all user input data when displaying it. If you do need to allow users to input HTML and JavaScript, then when you print it out, make sure to escape it so that the browser does not interpret it as code.

- Escaping

  - To escape a character means to replace an HTML character with a combination of ASCII characters, which tells the client to display that character as is, and to not process it; this helps prevent malicious code from running on a page. These combinations of ASCII characters are called HTML entities.

-  Consider the following HTML: `<p>Hello World!<\p>`. 
  - Let's say we don't want the browser to read this as HTML. 
    - To accomplish this, we can escape special characters that the browser uses to detect when HTML starts and ends, namely < and >, with HTML entities. 
    - If we write the following: `&lt;p&gt;Hello World!&lt;\p&gt;`, then that HTML will be displayed as plain text instead.
