# e-sync

A framework for upgrading from e-mail to a direct peer connection. Protocols that use e-sync can be interactive or could consist of only a single message for peer discovery.

## 1. Overview

E-mail is the most widely adopted decentralized protocol in the world, and it's popularity is expected to grow in 2033[1]. E-mail was designed and deployed in 1971, and naturally has several limitations that restrict it's usage for wider data-intensive usage. 

[1] [Email is not dead.](https://emailisnotdead.com)

## 1.1 Terminology

An e-sync protocol begins when one e-mail **provider** is able to send an **end-to-end encrypted message** over SMTP to another e-mail address. This first message includes a **handshake payload** which includes necessary metadata to upgrade the connection to a direct connection.

## 1.2 Handshake

E-sync uses two e-mail messages to establish a handshake between two e-mail addresses. The initiator sends the first message, which is a payload that includes a unique 32-byte token as well as a connection payload that includes the IP address, port, and connection type. To prevent eavesdropping by third parties on these payloads, it is recommended to send this first e-mail is sent as an end-to-end encrypted message. 

The receiver and initiator will have a challenge over a pre-shared symmetric key which must be shared out-of-band. This prevents attacks where a private key has been compromised a MITM is attempting to hijack the direct connection between the two devices.

## 2. Message format

#### `type` 

The `type` record is a byte that defines the type of connection that should be
created (e.g., webrtc, tcp, udp).

|type | byte | 
---------------
| tcp | 0x01 |
| udp | 0x02 |
| http | 0x03 |
| ftp | 0x04 |

#### `token`

The `token` record is a random value that makes it easier for clients to avoid
connecting to themselves. If a client sees a response with the same token as
a response they just sent out, they will know it came from them and ignore it. 

#### `discovery key`

The discovery key is a hash of the pre-shared symmetric key. It should be a 32-byte buffer encoded as hex.

#### `location`

The `location` record is an IP address and port.

## 3. Connection




