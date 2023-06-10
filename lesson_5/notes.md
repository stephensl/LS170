# Transport Layer Security (TLS)

## Focus Areas

  ### TLS 
  - Provides secure message exchange over an unsecure channel. 
    - HTTP does not provide any means of secure message transfer.
  
  - Security
    - There are multiple aspects to security.
    - TLS provides numerous services
      - Each addresses particular problem. 

  - Main foci
    - Understanding where HTTP is lacking in terms of secure message exchange.
    - Understanding how TLS works, and services offered. 
    - Understanding the problems related to security, and develop mental model of TLS approach. 


## Transport Layer Security (TLS) Protocol 
  - Started as SSL (Secure Sockets Layer)
  
  - Security Services
    - Encryption
    - Authentication
    - Integrity


### Encryption
  - Process of encoding message so it can only be read by those with an authorized means of decoding the message. 

### Authentication
  - Process to verify the identity of a particular party in the message exchange. 

### Integrity 
  - Process to detect whether a message has been interfered with or faked. 

#### It is not mandatory for an application which uses TLS to use all three of these services simultaneously. However, in practice, all three services generally used together to provide secure connection. 



### TLS Encryption
  - Types of Encryption
    - Symmetric Key Encryption
      - both parties have same secret key
      - key used for encryption and decryption
    - Asymmetric Key Encryption
      - also known as Public Key Encryption
      - uses pair of keys
        - public key to encrypt a message
        - private key to decrypt 

  - TLS Handshake
    - Process by which the initial secure connection is set up.

    - Problem: 
      - We want both HTTP request and response to be encrypted and only decrypted by intended recipient.

    - Approach: 
      - Uses combination of symmetric and asymmetric key encryption.
      - Initial symmetric key exchange is conducted using asymmetric key encryption.
        - Bulk of message exchange conducted via symmetric key encryption once received. 

    - Implementation: 
      - TLS assumes TCP is being used at the Transport Layer.
      - TLS handshake takes place after the TCP Handshake.
      
      1. TLS Handshake begins with `ClientHello` message sent immediately after the TCP `ACK`. 
        - Message contains:
          - maximum version of TLS protocol client can support
          - list of Cipher Suites client is able to use
          - additional information

      2. Upon receiving the `ClientHello` message, server responds. 
        - Message includes 
          - a `ServerHello` message 
            - sets the protocol version
            - sets Cipher Suite
            - additional information
          - Certificate 
            - Contains public key
          - a `ServerHelloDone` marker
            - indicates to client that finished this step of handshake.

      3. Once client receives `ServerHelloDone` marker, it will initiate key exchange process. 
        - Key exchange enables client and server to securely obtain a copt of the symmetric encryption key.
          - symmetric key generation dependent key exchange algorithm selected as part of Cipher Suite
          - Example using RSA: 
            - Client generates "pre-master secret" encrypts using server's public key, and sends to server.
            - Server receives encrypted "pre-master secret" and decrypts is using private key.
            - Client and server use "pre-master secret", along with pre-agreed parameters to generate the same symmetric key.
            - As part of communication which includes the `ClientKeyExchange` message (pre-master secret), client also sends a `ChangeCipherSpec` flag.
              - tells server that encrypted communications should now start using symmetric key. 
              - also includes `Finished` flag to indicate that client is done with TLS Handshake.
      
      4. Server also sends message with `ChangeCipherSpec` and `Finished` flags. 
        - Client and server can now begin secure communication using symmetric key. 

  ### Key Points from TLS Handshake
    - Agree which version of TLS to use in establishing secure connection. 
    - Agree on the various algorithms that will be included in Cipher Suite.
    - Enable exchange of symmetric keys that will be used for message encryption. 
    - Performance implications of up to two round-trips of latency.
      - Prior to any application data being sent. 
      - In addition to initial round trip resulting from TCP Handshake.

  ##### For UDP, rather than TCP at the Transport Layer, use protocol called Datagram Transport Layer Security (DTLS)


  ### Cipher Suites
    - Cipher
      - cryptographic algorithm 
      - steps for performing encryption, decryption, and related tasks.
    - Cipher suite is a set of ciphers. 

  #### Cipher Suite use in TLS
    - different ciphers used for different aspects of establishing and maintaining a secure connection. 
      - many algorithms can be used for key exchange, authentication, symmetric key encryption, integrity, etc. 
        - the algorithms performing these tasks, when combined, comprise the cipher suite. 
    - the suite to be used is agreed upon as part of TLS handshake.
      - As part of `ClientHello` message, client sends list of algorithms it supports for each required task. 
      - server chooses from these according to which algorithms it also supports. 



## TLS Authentication
  - Encryption may allow for messages to only be accessed by the intended recipient, but how do we know that the message is actually coming from a trusted source?

  - Certificate
    - During the TLS Handshake as part of its response to the `ClientHello` message, server provides its certificate. 
      - Certificate contains: 
        - Public Key (client uses during key exchange process)
        - Identification information
      - Certificates are publicly available, and therefore don't provide much authentication power alone.
        - Certificate and public key it contains, are only one part of an overall authentication system. 
      
  - General Implementation 
    - Server sends its certificate, which includes its public key. 
    - Sever creates signature in form of some data encrypted with server's private key. 
    - Signature is transmitted in a message along with the original data from which signature was created. 
    - On receipt of message, client decrypts signature using server's public key and compares decrypted data to original version. 
    - If two versions match, the encrypted version could only have been created by party in possession of private key. 

  #### We can now identify that the server which provided the certificate during the initial part of the TLS Handshake is in possession of the private key, and therefore the actual owner of the certificate. 

  **Problem Remains**
    - What if malicious third party created fake key/pair certificate?
    - How do we know if it is genuine?


  ### Certificate Authorities and Chain of Trust
    - Certificate Authorities 
      - Verifies that party requesting the certificate is who they say they are. 
      - Digitally signs the certificate being used. 
        - Usually done by encrypting some data with CA's own private key and using encrypted data as signature. 
        - Encrypted data is decrypted with CA's public key and compared with un-encrypted data. 
    - Who are Certificate Authorities?
      - Different Levels
        - Often hierarchy between issuers based on level.
        - Intermediate CA
          - Any company or body authorized by a Root CA to issue certificates on its behalf. 
            - Example: Let's Encrypt, Google Internet Authority
        - Root CA
          - Root certificates are self-signed and are essentially the end-point of the chain of trust. 
          - When receiving a certificate for checking, the browser can go up the chain to the Root Certificate stored in its list.

  ### The purpose of this chain-like structure is the level of security it provides. The private keys of the Root CAs are kept behind many layers of security in order to be kept as inaccessible as possible. As such they don't issue end-user certificates, but leave that up to the Intermediate CAs. Additionally, if the private key of an Intermediate CA somehow became compromised, the root CA can revoke the certificate for Intermediate, therefore invalidating all of the certificates down the chain from it, and simply issue a new one.

  ### Root CAs are essentially a small group of organizations approved by browser and operating system vendors.

  ### Ultimately this system still relies on trust, and as such isn't infallible. 




  ## TLS Integrity 
    - Provides functionality to check the integrity of the data being transported via the protocol. 

  ### TLS Encapsulation 
    - OSI defines TLS as a Session Layer protocol
    - Operates between HTTP (Application Layer) and TCP (Transport Layer).
    - TLS encapsulates application data in the same way that we've seen with other PDUs. 
      - Data to be transported forms a *payload* and the meta data is attached in the form of header/trailer fields. 
      - Main field of interest in terms of message integrity is `MAC` field.
        - `MAC` stands for Message Authentication Code. (*unrelated to MAC Address* (Media Access Control))


  ### Message Authentication Code (MAC)
    - `MAC` field is similar to checksum fields seen in other PDUs with difference in implementation/intention.
      - checksum field in TCP segment intended for error detection (testing if data was corrupted in transport)
        - intention of `MAC` field in TLS record is to add layer of security
          - provides means of checking that the message hasn't been altered or tapered with in transit. 

    - Implementation:
      - Uses hashing algorithm.
        1. sender creates a *digest* of data payload.
          - small amt of data derived from actual data that will be sent in the `MAC` field. 
          - created using specific hashing algorithm combined with pre-agreed hash value. 
          - hashing algo and hash value will have been agreed as part of TLS Handshake process when Cipher Suite is negotiated. 

        2. Sender will: 
          - encrypt data payload using the symmetric key 
          - encapsulate it into a TLS record
          - pass record down to the Transport Layer to be sent to the other party

        3. Upon receipt, receiver will: 
          - decrypt data payload using symmetric key
          - create digest of the payload using same algo and hash value
          - if digest created by receiver matches digest received in `MAC` field, message integrity confirmed.



  ## Summary 
    - HTTP requests and responses are transferred in plain text. 
      - This makes these messages essentially insecure.

    - We can use Transport Layer Security protocol to add security to HTTP communications. 

    - TLS encryption allows us to encode messages.

    - TLS encryption uses combination of Symmetric/Asymmetric Key Encryption. 
      - Encryption of initial key exchange is asymmetric, subsequent symmetrically encrypted. 

    - TLS Handshake is process by which client and server exchange encryption keys. 

    - TLS Handshake must be performed before secure data exchange can begin.
      - Involves several round trips of latency and has impact on performance. 

    - Cipher Suite
      - agreed set of algorithms used by client and server during secure message exchange. 

    - TLS Authentication
      - means of verifying the identity of a participant in message exchange. 
      - implemented through use of Digital Certificates
    
    - Certificates are signed by a Certificate Authority
      - work on basis of CHain of Trust which leads to small group of highly trusted Root CAs. 

    - Servers certificate is sent during TLS Handshake.

    - TLS Integrity
      - means of checking whether a message has been altered or interfered with in transit.
      - implemented through use of a Message Authentication Code (MAC)
      