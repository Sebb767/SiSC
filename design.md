# SiSC (Simple Storage Cluster) Design

Note that this software is currently in planning phase, not even alpha. You can't use the alpha and complain about bugs by now, so if you're not interested in aiding the development, come back at a later time.

## Basic Design

SiSC will be designed for very easy scaleability, yet it should allow an easy setup and easy network extension for home users (like me). To archieve this, SiSC will be a network of services for Storage (on per storage unit/file system), User Access (replicated Master) and a Control Unit (Master). To aid Systems behind a firewall, a relay node may also be implemented.

## Protocol

Yet none defined. It should however fullfill the following requirements:
- It should allow transportation of text (json?) message for inter-node requests and communication.
- It should be efficient for binary file transportation.
- Encryption has to be possible.

It should also be possible to access the master node (and UA nodes) by a different protocol (http probably) for user interaction (administration and file down-/uploading). HTTP is still an option since this would avoid rolling a own protocol, but on the other hand the overhead is sick. Maybe a protocol agnostic framework design would be the right way.

## Services

### Common Design

All nodes should generate an RSA Keypair on creation. This will be used for encryption and node identification. Nodes have specific rights assigend to them. Also, each server will have an instance, cluster and site value which will be used for replication rules (i.e. two clusters on two sites each on diffrent instances). Instance is a server or a VM host. Cluster describes the server cluster location in a site. The location should be the whole serer farm. Of course, these values may be ignored or used diffrently.

### Master Service

The master node is the only one allowed to issue right changes and to tell nodes to trust other nodes. If this node is compromised, the server is compromised. All right updates will be signed (here: encrypted) with the master's private key.

The master node should run a http backend or allow to be controlled by one in order to easily configure storage.

### User Access Service

Replicated master nodes, but they only supply read-only data. More of a cache. Since these are only useful in larger or HA clusters, their implementation is no priority.

### Storage Service

Storage Service instances will use exactly one specific path on the system they're running on as storage space. They will sync all their files there, as long as storage space is sufficient.

Configuration Nodes 

### Proxy Service

No target for now. Should allow to traverse firewalls, i.e. by keeping a persistent connection between two nodes.

## Rights Managment

## Data Storage

There should be three categories of data stored:

### System Metadata

This includes user profiles, public keys (of users and servers) & configuration. This will be usually be stored on the service location.

### File Metadata

References on previous file version, public key used for encryption, hash and replication status. Stored at the files.

### Actual Data

Nothing unexpected. Data stored on the given file system. Maybe encrypted, may be encrypted twice (storage node encryption, user encryption).
