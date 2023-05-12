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

  



