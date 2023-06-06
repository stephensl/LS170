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
    - Different applications or processes can be thought of as distinct *channel* for communication on a host machine
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

  - In this course, what we're primarily interested in is the concept of a socket and to a lesser extent the application of this concept for inter-network communication between networked applications, i.e. Internet Sockets. We're not going to look too much into the implementation detail of how Internet Sockets work. One important thing to be clear on though is that **there is a distinction between the concept of a network socket and its implementation in code.**
    - Conceptually a socket is a communication end-point defined by Address/Port pair. 

  ### To allow many processes within a single host to use TCP communication simultaneously, the TCP provides a set of addresses or ports within each host. Concatenated with the network and host addresses from the internet communication layer, this forms a socket. 

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
  - In a connectionless system we could have one socket object defined by the IP address of the host machine and the port assigned to a particular process running on that machine. 
  - That object could call a listen() method which would allow it to wait for incoming messages directed to that particular IP/port pair. 
    - Such messages could potentially come from any source, at any time, and in any order, but that isn't a concern in a connectionless system -- it would simply process any incoming messages as they arrived and send any responses as necessary.

- Connection-Oriented
  - A connection-oriented system would work differently. 
  - You could have a socket object defined by the host IP and process port, just as in the connectionless system, also using a listen() method to wait for incoming messages.
    - the difference in implementation would be in what happens when a message arrives. 
  - At this point we could instantiate a new socket object; this new socket object wouldn't just be defined by the local IP and port number, but also by the IP and port of the process/host which sent the message. 
    - This new socket object would then listen specifically for messages where all four pieces of information matched
      - source port 
      - source IP
      - destination port
      - destination IP
        - The combination of these four pieces of information is commonly referred to as a *four-tuple*.

  - Any messages not matching this four-tuple would still be picked up by the original socket, which would then instantiate another socket object for the new connection.


  - Implementing communication in this way effectively creates a dedicated virtual connection for communication between a specific process running on one host and a specific process running on another host. 
  - The advantage of having a dedicated connection like this is that it more easily allows you to put in place rules for managing the communication such as the order of messages, acknowledgements that messages had been received, retransmission of messages that weren't received, and so on. 
    - The purpose of these types of additional communication rules is to add more reliability to the communication. 



## Network Reliability

  - The network up to, and including, the Internet Protocol is effectively unreliable as communication channel. 
    - Protocols such as Ethernet or IP include checksum data as part of header or trailer to test for corruption
      - If data is corrupt, it is dropped, and no mechanism for replacing lost data.
        - Possibility of data being lost and not replaced makes network up to IP unreliable. 

  - NEED
    - system of rules (protocol) for ensuring that all data sent is received at the other end in correct order. 

  ### Building a Reliable Protocol 

    - Version 1: 
      - Problem: Messages can be corrupt or lost
        - How can we ensure message has been successfully received?
      - Solution: Use an acknowledgement message.
        - Sender sends one message at a time
        - If message is received, receiver sends an acknowledgement
        - When acknowledgement is received, sender sends next message. 
          - Example: 
            - Two people on phone, giving credit card info
              - Person A: '3795'
              - Person B: 'got it' 
              - Person A: '4632'
              - Person B: 'yep'
              - Person A: ...
      - Flaw: 
        - Sender may not receive acknowledgement
          - recipient never receives message, so does not send acknowledgement message
          - recipient receives, sends acknowledgement, acknowledgement corrupted or lost
            - Sender will not send next message

    - Version 2: 
      - Problem: Acknowledgement not received
      - Solution: re-send the message is acknowledgement not received within certain time-frame.
      - Rules: 
        - Sender sends one message at a time, and sets a timeout
        - If message received, receiver sends acknowledgement
        - When acknowledgement received, sender sends next message
          - If acknowledgement not received before timeout expires, sender assumes message or acknowledgement are missing and sends the same message again
      - Flaw: 
        - Duplication 
          - Receiver receives message and sends acknowledgement
            - Acknowledgement becomes corrupt or lost 
            - Acknowledgement is delayed and sender doesn't receive before timeout expires
          - Sender re-sends message that receiver has already received
            - How would receiver know it is a duplicate?

    - Version 3: 
      - Problem: message received but acknowledgement is not received or not in time, results in duplicate message.
      - Solution: add sequence numbers to the message
      - Rules: 
        - Sender sends one message at a time with sequence number and sets a timeout
        - If message received, receiver sends an acknowledgement which uses the sequence number of the message to indicate that it was received
        - When acknowledgement is received, sender sends next message in sequence
          - If acknowledgement not received before timeout expires, sender assumes message or acknowledgement are missing, and sends the same message with teh same sequence number. 
          - If recipient receives a message with a duplicate sequence number, assumes the sender never received the acknowledgment and sends another acknowledgement for that sequence number
            - Discards duplicate. 

      ### Version 3 provides fundamental elements required for reliable data transfer
        - In-order delivery
          - data received in order it was sent
        - Error detection
          - corrupt data is identified using a checksum
        - Handling data loss
          - missing data retransmitted based on acknowledgements and timeouts
        - Handling duplication
          - duplicate data is eliminated through the use of sequence numbers

        ### Limitations at this point
          - Not efficient: Stop and Wait protocol
            - Each message sent one at a time
            - Acknowledgement received before next message is sent
            - Waiting for acknowledgement is not efficient use of bandwidth

    - Throughput vs Bandwidth 
      - Throughput 
        - actual amount of data that is successfully transmitted or processed over a network, system, or device within a given time frame. 
        - actual flow of water through the pipe
      - Bandwidth 
        - describes the theoretical maximum capacity of a network link
        - water pipe total capacity

  ### Pipelining for Performance
    - sending multiple messages one after the other without waiting for acknowledgement
      - Still reliable as acknowledgement still sent, and retransmission can still occur. 
    - multiple messages are being transferred at any one time. 
    - Example: 
      - Non-pipelined
        - A: 'hey'
        - B: 'hey back' 
        - A: 'how are you?'
        - B: 'good thanks'
      - Pipelined
        - A: 'hey'
             'how are you?'
        - B: 'hey back'
             'good thanks'

    - Different ways of implementing pipelined approach:
      - Go-back-N
        - the sender maintains a sliding window of messages. The window represents the maximum number of unacknowledged messages that can be in transit at any given time. The sender continues sending messages within the window until it receives acknowledgements for all messages within the window or a timeout occurs. If a timeout occurs, the sender re-sends all unacknowledged messages within the window.
      
      - Selective Repeat
        - This protocol is similar to Go-Back-N but provides more flexibility. The sender maintains a window of messages and waits for acknowledgements individually. If an acknowledgement is not received for a particular message within a timeout period, only that specific message is retransmitted, not all messages within the window.
      
      - Both systems the sender will implement a 'window' representing the maximum number of messages that can be in the pipeline at any one time. 
        - Once it has received appropriate acknowledgements for the messages in this window, it moves the window on, allowing new messages to be sent.

      
    - Benefits: 
      - Efficient use of available bandwidth
        - overlapping the transmission and acknowledgement processes
        - more time is spent actually transmitting data vs waiting for acknowledgements

    - Balancing:
      - Finding balance between performance and reliability is a major part of the implementation of the Transmission Control Protocol (TCP). 



## Transmission Control Protocol (TCP)
  - Provides reliable data transfer.
    - TCP must recover data that is damaged, lost, duplicated, or delivered out of order by the internet communication system.
  - Provides data encapsulation and multiplexing
    - Uses TCP segments 
    
### Abstraction of data reliability
  - TCP provides the abstraction of reliable network communication on top of an unreliable channel. 
    - Hides complexity of reliable network communication from the application layer.
      - Data integrity
      - de-duplication 
      - in-order delivery
      - re-transmission of lost data

### TCP Segments 
  -  Segments 
    - Protocol Data Unit (PDU) of TCP.
    - Utilizes headers, and payload to provide encapsulation of data from layer above. 

  ### TCP Segment Header
    - Source Port and Destination Port
      - Provide multiplexing capability 
    - CHECKSUM
      - Error Detection aspect
      - Sender generates value using algorithm
      - Receiver generates value using same algo
      - If do not match, segment is dropped
      - Makes Checksum at lower layers redundant
    - Sequence Number and Acknowledgement Number 
      - Provides for:
        - In-order delivery 
        - Handling data loss
        - Handling duplication 
    - Window Size 
      - Related to Flow Control 
    - Flag Fields 
      - One-bit boolean fields
      - URG/PSH 
        - Related to how data contained in the Segment should be treated in terms of importance/urgency.
      - SYN, ACK, FIN, RST 
        - used to establish and end a TCP connection
        - manages the state of the connection 

### TCP Connections 
  - TCP is a connection-oriented protocol.
    - Does not send application data until a connection has been established between application processes.
  - To establish a connection, TCP uses 3-way handshake.
    - Sender sends a SYN message. (TCP segment with SYN flag set to 1)
    - Upon receiving SYN message, receiver sends back a SYN ACK message. (TCP segment with  SYN nad ACK flags set to 1)
    - Upon receiving the SYN ACK, sender then sends an ACK. (TCP segment with ACK flag set to 1)
    - Upon sending the ACK, the sender can immediately start sending application data.
      - The receiver must wait until it has received the ACK before it can send any data back to sender.
  - This process used to synchronize (SYN) the sequence numbers that will be used during connection. 

  ### Managing Connection State 
    - Another use for flags is to manage the state of the connection. 
    - Connection progresses through series of states:
      - *LISTEN*
      - SYN-SENT
      - SYN-RECEIVED 
      - *ESTABLISHED*
      - FIN-WAIT-1
      - FIN-WAIT-2
      - CLOSE-WAIT
      - CLOSING
      - LAST-ACK
      - TIME-WAIT
      - Fictional state: CLOSED (no connection exists)
    - Most concerned with ESTABLISHED and LISTEN on the server side.
      - Other states are related to establishing and terminating the connection.

  
  ### 3-way Handshake to Establish a Connection, with Connection States

| Client Start State | Client Action                                             | Client End State | Server Start State | Server Action                                                        | Server End State |
| ----------------- | -------------------------------------------------------- | ---------------- | ------------------ | -------------------------------------------------------------------- | ---------------- |
| CLOSED            | Sends a SYN Segment                                       | SYN-SENT         | LISTEN             | Waits for a connection request                                        | -                |
| SYN-SENT          | Waits to receive an ACK to the SYN it sent, as well as the server's SYN | SYN-SENT   | LISTEN             | Sends a SYN ACK Segment which serves as both its SYN and an ACK for the client's SYN | SYN-RECEIVED     |
| SYN-SENT          | Receives the SYN ACK Segment sent by the server, and sends an ACK in response. The client is now finished with the connection establishment process | ESTABLISHED | SYN-RECEIVED       | Waits for an ACK for the SYN it just sent                             | -                |
| ESTABLISHED       | Ready for data transfer. Can start sending application data | ESTABLISHED      | SYN-RECEIVED       | Receives the ACK sent in response to its SYN. The server is now finished with the connection establishment process | ESTABLISHED      |



### Key Points in 3-way Handshake
  - Sender cannot send any application data until after it has sent the `ACK` Segment.
    - There is a round-trip of latency before any application data can be exchanged.
      - Since this occurs every time a TCP connection is made, impacts any application which uses TCP at Transport Layer.
  - TCP involves a lot of overhead in establishing connection and providing reliability through retransmission of lost data.
    - Overhead refers to additional procedures and data that are required to ensure:
      - reliable
      - ordered
      - error-checked delivery
    - Overhead includes:
      - establishing connections
      - retransmitting lost data
      - controlling flow of data
      - avoiding network congestion
  - **Since TCP requires significant overhead in providing its service, it is important that the actual data transmission is as efficient as possible.**

### Flow Control 
  - Problem: 
    - Receiver can only process a certain amount of data in a particular time-frame.
    - If a receiver receives too much data at once, it is stored in a buffer. 
      - Buffer size depends on amount of memory allocated according to the OS and physical resources available. 
  - Solution:
    - Each side of connection lets the other know amount of data it can accept via the `WINDOW` field of the TCP header. 
      - The `WINDOW` is dynamic and may change during the course of a connection.
        - If receiver's buffer is getting full, it can set a lower amount in the `WINDOW` field of a Segment sent to the sender.
          - Sender can then reduce the amount of data it sends accordingly. 
  - Limitations: 
    - Although prevents sender from overwhelming the receiver...
      - Does not prevent sender or receiver from overwhelming the underlying network. 
        - For this, we need a mechanism for Congestion Avoidance.

### Congestion Avoidance
  - Occurs when more data being transmitted on the network than its capacity to process and transmit the data. 
    - Similar to traffic jam, but excess vehicles are simply lost. 
  - In IP packets moving across network in series of hops:
    - At each hop, packet is processed
      - Router at the hop runs checksum
      - Checks destination address for routing purposes
    - Routers use buffer to store data awaiting processing, and drops packet if buffer overflows
  - TCP 
    - Re-transmits lost data, which may lead to lots of retransmission occurring if network is congested.
      - In order to avoid excessive re-transmission, TCP uses data loss as feedback mechanism to detect and avoid congestion.
        - If lots of re-transmissions occurring, TCP interprets congestion and reduces size of transmission window. 
    - Various approaches and algorithms for determining size of initial transmission window.
      - Exact implementation dependent on which variant of TCP is being used. 

### Limitations/Disadvantages of TCP
  - Latency overhead in establishing connection due to Handshake process. 
  - Head of Line Blocking (HOL)
    - General networking concept not specific to TCP
    - Issues in delivering of processing one message in a sequence of messages can delay or block the delivery or processing of subsequent messages in the sequence. 
    - TCP is vulnerable to this as it provides for in-order delivery of Segments. 
      - If one segment goes missing, must be retransmitted
      - Segments that come after cannot be processed until retransmission has occurred
        - Leads to queuing delays- one of the elements of latency. 



## User Datagram Protocol (UDP)
  - PDU known as Datagram 
  - Encapsulates data from layer above into a payload, then adds header information.

  ### UDP Headers
    - 4 fields
      - Source Port 
      - Destination Port 
      - UDP Length (length in bits of Datagram, including any encapsulated data)
      - Checksum field for error detection.
        - Optional if using IPv4 at the Network layer
        - IPv6 must include Checksum in Datagram since IPv6 packets do not include one themselves.

  ### UDP vs TCP 
    - Similarities: 
      - Both provide multiplexing in the same way through use of Source and Destination Port numbers. 
    - Differences:
      - Connectionless protocol. 
      - Does not address unreliability of layers below it.
      - No guarantee of message delivery. 
      - No guarantee of message delivery order.
      - No built-in Congestion Avoidance.
      - No built-in Flow Control 
      - No connection state tracking (connectionless).

    ### Why use UDP?
      - Simplicity 
        - Provides speed and flexibility.
      - Connectionless
        - Applications using UDP at Transport layer can start sending data without waiting for connection to be established. 
        - Lack of acknowledgement means faster data delivery.
          - Reduced latency without acknowledgement data.
      - No in-order delivery
        - Removes HOL issue (at least at Transport layer)
      - Flexibility 
        - Engineer can decide services and implementation based on use-case
          
      
      - Examples: 
        - Want in-order delivery but not worried about occasional piece of lost data.
          - Implement sequencing, but not re-transmission. 
          - Services can be implemented at Application layer, using UDP as a *base template* to build on. 
        - Voice or Video Calling Application 
          - Occasional piece of lost data may result in small glitch or missing pixel
            - tradeoff of speed vs complete data reliability.
        - Gaming 
          - small glitch preferred over lag-time. 
    

    **UDP provides increased flexibility and freedom to developers, but various best-practices should be adhered to.** 
      - Example: 
        - UDP-based application should provide some form of congestion avoidance in order to prevent overwhelming network. 


## Summary 

  - Multiplexing/Demultiplexing 
    - provide for transmission of multiple signals over a single channel.
    - enabled through use of network ports. 
  
  - Network Sockets
    - combination of IP address and Port Number 
    - at implementation level, network sockets can also be *socket objects*. 
  
  - Underlying Network Unreliable
    - if we want reliable data transfer, must implement a system of rules to enable it. 
  
  - Transmission Control Protocol (TCP)
    - connection-oriented protocol. 
    - establishes connection using 3-way handshake.


  - TCP provides reliability through:
      - message acknowledgement 
      - retransmission 
      - in-order delivery 
    
  - TCP provides Flow Control and Congestion Avoidance.

  - TCP Limitations 
    - latency overhead in establishing connection.
    - potential Head-of-Line Blocking (HOL) as result of in-order delivery. 

  - User Datagram Protocol (UDP)
    - connectionless 
    - very simple compared to TCP
    
  - UDP Positives
    - provides multiplexing
    - provides speed and flexibility 

  - UDP Tradeoffs 
    - no reliability 
    - no in-order delivery 
    - no flow control 
    - no congestion avoidance


