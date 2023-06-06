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