# autopeers

A specification for upgrading to peer-to-peer connections.

#### type 

The `type` record is a byte that defines the type of connection that should be
created (e.g., webrtc, tcp, udp).

#### token 

The token record is a random value that makes it easier for clients to avoid
connecting to themselves. If a client sees a response with the same token as
a response they just sent out, they will know it came from them and ignore it. 

#### data

Fields based on the type.  

## fields for data types


#### tcp


#### udp

#### webrtc


