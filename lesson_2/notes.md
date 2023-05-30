# Transport Layer 

## Focus Areas
  - Transport Layer is key to comprehending how networked applications communicate with each other. 
  
  - How transport layer protocols enable communication between processes
    - Mental models for: 
       - multiplexing
       - demultiplexing 
       - how ports work with IP addresses to provide this functionality
    
  - Network reliability is engineered
    - Understanding internet and web are combinations of technologies
      - network reliability is an aspect of this.

  - Understand the trade-offs
    - TCP and UDP are the result of many different design decisions
      - design decisions generally involve a trade-off.
    - TCP / UDP service provision and tradeoffs between them. 



## Communication between Processes 

  - Internet as layered system of communication
  - Each layer provides a service to layer above
  - Modern networked applications need more than what IP can provide. 
    - Direct connection between applications
      - How can we provide end to end communication between applications or processes?
    - Reliable network communication

  
### Limitations of IP for Networked Applications
  - Internet Protocol and IP Addressing 
    - intended to provide communication between hosts or devices. 
      - hosts may be on the same local network, different local networks, or across the world.
        - We can use IP to move messages from one host to the other, but not more than that
  
  - Hosts (devices connected to network) can be running multiple applications at the same time.
    - Each of these applications may be sending and receiving data over the network. 
  - To distinguish between data fort different applications, transport protocols are utilized:
    - TCP 
    - UDP
  - These protocols use port numbers as each application is assigned a port number and incoming data is directed ot the appropriate application based on this port number. 
  - This allows multiple applications to share the network connection on a single host. 


### What problem needs to be solved here?
  - IP can only provide so much functionality in regard to sharing data between hosts.
    - Communication between an application running on one host and application running on another host?
    - Two different applications or processes running on the same host?


## Multiplexing and Demultiplexing 
  - There may be many networked applications running on a device at one time. 
    - These applications all want to be able to send and receive data simultaneously
      - Examples: 
        - Sending an email while listening to Spotify
        - Load a web-page while chatting in Slack
    - Different applications or processes can be thought of as distinct channel for communication on a host machine
    - With IP addresses we only have a single channel between hosts

  - Need a way to transmit multiple data inputs over this single host-to-host channel, then separate them out at the other end. 

  - Multiplexing: 
    - idea of transmitting multiple signals over a single channel
  - Demultiplexing
    - process of separating multiple streams of data that have been multiplexed together 
    - directs each stream to correct recipient based on info in the data stream (such as port number)

## Ports 
A port is an identifier for a specific process running on a host. 
  - Identifier is an integer in the range 0-65535
    - Sections of the range are reserved for particular purposes:
      - 0-1023
        - Well known ports assigned to processes that provide commonly used network services.
          - HTTP is port 80 
          - FTP is port 20 
          - SMTP is port 25
      - 1024-49151
        - Registered ports assigned as requested by private entities
           - Examples: Microsoft and IBM have ports assigned that they use to provide specific services
        - On some operating systems, ports in this range are used for allocation as ephemeral ports on the client side
      - 49152-65535
        - Dynamic ports (private ports)
        - Cannot be registered for a specific use.
        - Can be used for customized services or allocation as ephemeral ports


### The source and destination port numbers are included in the PDU for the transport layer. 
  - The name and exact structure of the PDUs varies according to the Transport Protocol used
    - All include the source and destination port.

  ### The IP address and the port number together are what enable end-to-end communication between specific applications on different machines.
    - This combination can be thought of as defining a communication end-point.
    - This end point is generally referred to as a *socket*.



### Postal service example: 
  - Apartment building has street address and numerous apartments within it. 
  - Mail delivered to apartment is separated by concierge and placed in particular mailbox based on apartment number/name. 
    - Street address of building is like IP address
    - Individual apartment numbers are like port numbers
  - Postal service acts as Internet Protocol and building concierge acts as Transport later protocol (TCP or UDP).



## Sockets 
  - Meaning may change depending on the context: 
    - Conceptually:   
      - abstraction for an endpoint used for inter-process communication.
    - Implementation:
      - UNIX socket
        - mechanism for communication between local processes running on the same machine.
      - Internet sockets
        - TCP/IP socket
          - mechanism for inter-process communication between networked processes (usually on different machines.)

  - In this course, what we're primarily interested in is the concept of a socket and to a lesser extent the application of this concept for inter-network communication between networked applications, i.e. Internet Sockets. We're not going to look too much into the implementation detail of how Internet Sockets work. One important thing to be clear on though is that there is a distinction between the concept of a network socket and its implementation in code.

  ### Implementation 
    - Involves instantiating socket objects. 
    - Sockets implemented as objects helps to understand how they can be used to create connections between applications.
      - Helps understand difference between connection-oriented communication and connection-less communication. 
        - Useful in understanding difference between TCP and UDP protocols. 

  
### Sockets and Connections
  - Example: 
    - Attempting to hold 5 separate conversations at once
    - Other party speaks at will, not waiting to see if listening or not. 
    
    - Imagine could replicate self to be totally present for each of 5 conversations
      - Creating *connection* between self and other participant.

  - This example is a simplified analogy of difference between connection-less and connection-oriented network communication.

    - **By instantiating multiple socket objects we can implement connection-oriented network communication between applications.**


- Connectionless 
  - In a connectionless system we could have one socket object defined by the IP address of the host machine and the port assigned to a particular process running on that machine. That object could call a listen() method which would allow it to wait for incoming messages directed to that particular IP/port pair. Such messages could potentially come from any source, at any time, and in any order, but that isn't a concern in a connectionless system -- it would simply process any incoming messages as they arrived and send any responses as necessary.

- Connection-Oriented
  - A connection-oriented system would work differently. You could have a socket object defined by the host IP and process port, just as in the connectionless system, also using a listen() method to wait for incoming messages; the difference in implementation would be in what happens when a message arrives. At this point we could instantiate a new socket object; this new socket object wouldn't just be defined by the local IP and port number, but also by the IP and port of the process/host which sent the message. This new socket object would then listen specifically for messages where all four pieces of information matched (source port, source IP, destination port, destination IP). The combination of these four pieces of information is commonly referred to as a four-tuple.

  Any messages not matching this four-tuple would still be picked up by the original socket, which would then instantiate another socket object for the new connection.


  - Implementing communication in this way effectively creates a dedicated virtual connection for communication between a specific process running on one host and a specific process running on another host. The advantage of having a dedicated connection like this is that it more easily allows you to put in place rules for managing the communication such as the order of messages, acknowledgements that messages had been received, retransmission of messages that weren't received, and so on. The purpose of these types of additional communication rules is to add more reliability to the communication. 