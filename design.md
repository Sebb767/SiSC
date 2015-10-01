# SiSC (Simple Storage Cluster) Design

Note that this software is currently in planning phase, not even alpha. You can't use the alpha and complain about bugs by now, so if you're not interested in aiding the development, look back at a later time.

## Basic Design

SiSC will be designed for very easy scaleability, yet it should allow an easy setup and easy network extension for home users (like me). To archieve this, SiSC will be a network of services for Storage (on per storage unit/file system), User Access (replicated Master) and a Control Unit (Master). To aid Systems behind a firewall, a relay node may also be implemented.

## Protocol

Yet none defined. It should however fullfill the following requirements:
- It should allow transportation of text (json?) message for inter-node requests and communication.
- It should be efficient for binary file transportation.
- Encryption has to be possible.

It should also be possible to access the master node (and UA nodes) by a different protocol (http probably) for user interaction (administration and file down-/uploading). 

## Services

tbd