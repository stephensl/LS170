# The Internet

### Goals
- Build a mental model of communication between networked applications as the interaction of multiple different systems of rules (protocols). 
- Build general picture of network infrastructure
- Awareness of limitations of physical network
  - dependent on underlying infrastructure
    - bandwidth, latency
- Protocols 
  - logical sets of rules designed to support network functionality. 
- IP (Internet Protocol) enables communication between devices. 


## What is the internet?
  - A network of networks that facilitates the sharing of information across devices. 
  - A vast number of networks connected together. 
  - Systems of routers direct traffic between sub-networks 

  ### What is a network?
    - A network is formed by two or more devices that are connected in a way that allows for communication and data sharing. 
      - Basic level: 
        - Connecting two computers with a LAN cable and configuring to form distinct network. 

  ### What is LAN or WLAN? 
    - Local Area Network 
      - Multiple devices connected to a network switch or hub. 
        - Communication limited to only those devices that are connected to the switch/hub. 
    - Wireless Local Area Network
      - Devices are connected wirelessly to hub or switch that connects devices as part of its network.

  ### Inter-network 
    - Communication between networks.
    - Utilize **routers** to direct network traffic to other networks. 
      - Within a LAN, routers play the role of gatekeepers into and out of the network. 
      - Systems of routers direct traffic between sub-networks.


## Routers vs Switches 
  - Switches are used to connect multiple devices to the same network.
  - Routers are used to connect multiple networks. 


## Protocols 
  - A set of tules that govern the exchange or transmission of data. 
  - Many protocols are used to communicate on over the internet. Popular ones include: 
    - IP
    - SMTP 
    - TCP 
    - HTTP
    - Ethernet
    - FTP
    - DNS
    - UDP 
    - TLS 

### Why so many protocols for network communication?
  - To address different aspects of network communication.
  - To address the same aspect of network communication, but differently for particular use case.

### Protocols for different aspects of communication
- Example: human speech 
  - When we speak we can treat grouping of words as single message within a conversation. 
  - In order to ensure understanding, we must correctly order the words within that message. 
    - ASPECT: Word order is part of the *syntactical rules* that govern the structure of the message. 
    - ASPECT: Flow and order of messages in the conversation are *message transfer rules* for how to conduct speech.

### Different Protocols for same aspect of communication.
  - Example: Asking questions in school vs casually with friends
    - Student asking question to teacher in class follows one Protocol of message transfer rules: 
      1. Raise hand
      2. Teacher acknowledges student
      3. Student asks question 
      4. Teacher answers question. 
    - Asking the same question to friends requires a different protocol. 
      1. Nudge friend with elbow
      2. Ask question casually
      3. Receive answer
    - Presenting at conference
      1. Set time to present
      2. Stand and project message to audience
      3. Allow for questions. 
      4. Complete in designated time.
  - These are concerned with the same aspect of communication: the flow and order of message transfer, however they use different sets of rules or *protocols*. 









## Layered System
  - Useful to group protocols that address a particular aspect of communication. 
  - We can think of protocol groups as functioning within layers of an overall system of communication. 

### Example of verbal communication in protocol group layers
- We modularize and structure communication into a layered system in order to analyze each facet of the process. 
  - Logical message structure
    - Linguistic rules for how to structure a message
      - word order
  - Logical message transfer 
    - Etiquette rules for transfer of individual messages from one person to another.
      - initiating conversation
      - taking turns to speak
  - Physical message creation and interpretation
    - The physics and biology of speech and hearing
      - control of vocal chords
      - function of the ear
  - Physical message transfer
    - Transfer of message across physical medium. 
      - sound waves carried through the air

  
### Application to network communication
- Two most popular models:
  - OSI (Open Systems Interconnection)
  - TCP/IP (Internet Protocol Suite)
- There is overlap between the layers of the two models


## OSI 
- Application 
- Presentation 
- Session 
- Transport
- Network 
- Data Link
- Physical 

## TCP/IP
- Application (maps to top three layers of OSI model)
- Transport   (mostly maps to fourth layer of OSI model (Transport))
- Internet    (mostly maps to third layer of OSI (Network))
- Link        (mostly maps to bottom 2 layers of OSI model (Data Link and Physical))
 

### Why different number of layers?
  - Each model uses different approach:
    - OSI divides layers in terms of the functions that each layer provides.
      - Physical addressing, logical addressing and routing, encryption, compression, etc.
    - Internet Protocol Suite divides layers in terms of scope of communication within each layer
      - Within local network, between networks, etc. 

  - No single model will perfectly fit real-world implementation. 


## Data Encapsulation
  - Hiding data from one layer by encapsulating it within a data unit of the layer below. 

  ### Protocol Data Units (PDU)
    - An amount or block of data transferred over a network. 
    - Different protocols or protocol layers refer to PDUs by different names:
      - Link/Data Link layer: PDU is known as a *frame*
      - Internet/Network layer: PDU known as a *packet*
      - Transport layer: PDU known as a *segment* (TCP) or *datagram* (UDP)

  ### Basic concept of PDUs is the same: 
    - PDU consists of: 
      - header
      - data payload
      - trailer/footer (in some cases)

    ### Header and Trailer
      - Purpose: to provide protocol-specific metadata about the PDU.
        - Exact structure of header and possible trailer varies from protocol to protocol. 
        - Example: 
          - Internet Protocol packet header:
            - Includes fields for the Source IP Address and the Destination IP Address to correctly route the packet. 

    ### Data Payload 
      - The data we want to transport over the network using a specific protocol at a particular network layer.
      - Data Payload is key to the way encapsulation is implemented. 
      - The entire PDU from a protocol at one layer is set as the data payload for a protocol at the layer below. 

      - Separation of layers provides level of abstraction that allows us to use different protocols at a certain layer without worrying about the layers below.
        - Example: 
          - In the Application layer, many protocols may be used depending on the application and use case. 
            - Email client would use SMTP
            - Web browser would use HTTP
            - File transfer program would use FTP
          - All of these programs could use TCP at the Transport layer to transfer the application layer data. 





## The Physical Network 
  - Review:
    - Protocols act as a system of rules for network communication.
    - Groups of protocols work in a layered system. 
      - Protocols at one layer provide services to layer above.
    - Data is encapsulated into PDUs (Protocol Data Units), creating separation between protocols operating at different layers.

### Bits and Signals 
  - OSI model defines a Physical layer as the bottom layer (layer 1)
  - Internet Protocol Suite doesn't concern itself directly with physical interfaces
    - Does include some physical functions in the Link layer. 
  
  - Functionality at this level: 
    - Concerned with transfer of bits (binary data).
      - In order to transport:
        - Bits are converted to signals.
          - Depending on transportation medium used, bits converted to: 
            - electrical signals
            - light signals
            - radio waves

### Characteristics of Physical Network
  - Latency
    - Measure of time taken to get from one point in network to another.

  - Bandwidth
    - Amount of data that can be sent in a particular unit of time (typically seconds)

  - Example: 
    - Single lane road with car traveling from one location to another. 
      - Distance is 10 miles between locations.
      - Max speed of car is 50 mph
      - 12 mins to travel from A to B
        - Road has a latency of 12 minutes.
    - Adding more lanes allows more cars to travel at once.
      - Increases bandwidth of the road.
      - Still takes 12 minutes to travel A to B, so latency is 12 mins still.

### Elements of Latency 
  - Generally thought of as a measure of delay.
    - Different types of delay determine the overall latency of a network connection.

      - Propagation Delay: 
        - amount of time for message to travel from sender to receiver
        - calculated as ratio between distance and speed
        - basically explained in car analogy

      - Transmission Delay:
        - data typically won't be transported across a single cable, and will travel many different wires/cables connected by switches/routers/etc.
        - Each of these elements within the network can be thought of as an individual 'link' within the overall system.
        - Transmission delay is the amount of time it takes to push data onto the link. 
          - In car analogy- time it takes to navigate an intersection or interchange between different roads. 

      - Processing Delay:
        - Data traveling across the physical network doesn't directly cross from one link to another, but is processed in various ways.
        - The time it takes to be processed is the processing delay. 
          - In car analogy, if at every interchange there was a checkpoint that required processing- like an ID check.

      - Queuing Delay: 
        - Network devices like routers can only process a certain amount of data at one time. 
        - If more data than device can handle, it queues or buffers the data. 
        - The amount of time the data is waiting in the queue to be processed is the queueing delay.
          - In car analogy, waiting in traffic to pass a checkpoint.

    ### Total Latency between two points, such as a client and server, is the sum of the delays above.
      - Value usually given in milliseconds (ms) 

  ### Additional Latency terms:
    - Last-mile latency
      - many delays can take place within the parts of the network that are closest to the end points. 
      - relates to delays involved in getting the network signal from ISP network to your home or office network. 
        - Hops within the core part of network are longer with less interruptions for transmission, processing, and queueing. 
        - At network edge, there are more frequent and shorter hops as data is directed down the hierarchy to the appropriate sub-network. 
          - Network edge can be thought of as the entry point into a network like a hom eor corporate LAN. 

    - Round-trip Time
      - Length of time for a signal to be sent, added to the length of time for an acknowledgement or response to be received. 

  

### Network Hops
  - Data does not move directly on the network from start to end point
    - Consists of several hops or journeys between nodes of the network
      - Nodes can be thought of as routers that process data and forward to next node on the path. 
  - Can run `traceroute google.com` (`tracert` for windows)
    - returns a list of hops taken for test data to get from machine to Google server. 
    - values indicate RTT for each hop. 
  

### Bandwidth 
  - Varies across network. 
    - Capacity of core network higher than part of infrastructure that ultimately connects to home or office. 
    - The bandwidth a connection receives is the lowest amount at a particular point in the overall connection. 
    - The point at which bandwidth changes from relatively high to relatively low is a bandwidth bottleneck. 
    - Low bandwidth can be an issue when dealing with large amounts of data
      - In many situations, latency can be a much more serious limitation on the performance of networked application.

### Limitations of Physical Networks 
  - The limitations of the physical network limitations can impact the way we utilize and make decisions about higher level protocols within our applications. 

  
