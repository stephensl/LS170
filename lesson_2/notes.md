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