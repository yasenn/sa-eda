# Peer Addressability via jenkov.com

[Peer Addressability](https://jenkov.com/tutorials/p2p/peer-addressability.html)

Once peers in a peer-to-peer network has addressed the [peer connectivity](https://jenkov.com/tutorials/p2p/peer-connectivity.html) challenge, the peers need a way to address each other, so a peer can specify precisely which other peer in the network it wants to communicate with. I refer to this as the _peer addressability_ challenge.

## Assigning GUIDs

Peer addressability is typically achieved by assigning a unique GUID to each peer in the network. The GUID is typically designed to work well with the chosen routing table design of the given P2P network routing algorithm. Different P2P routing algorithms thus have different GUID and routing table structures which give different characteristics.

For instance, Chord and Kademlia uses a number from 0 to N as GUID, where N is the maximum number of peers the network can contain. Typically a GUID of 64 bits (8 bytes), 128 bits (16 bytes), 160 bits (20 bytes) or 256 bits (32 bytes) is used.

### One-dimensional GUIDs

When a GUID consists of a single number, a single coordinate, it is essentially a one-dimensional GUID. Chord, Kademlia, Pastry and Tapestry all use a one-dimensional GUID. The diagram below shows an example of a P2P network using a one-dimensional GUID:

![A P2P network using a one-dimensional GUID space](https://jenkov.com/images/p2p/peer-addressability-1.png) 

### Multi-dimensional GUIDs

If a GUID consists of multiple numbers, multiple coordinates, that GUID is essentially multi-dimensional. Polymorph's P2P routing algorithms uses a GUID scheme where the GUIDs consists of multiple numbers - multiple coordinates.

A multi-dimensional GUID can either have fixed dimensionality or dynamic dimensionality. A GUID scheme with a fixed dimensionality means a GUID scheme where all GUIDs have the same number of dimensions. A GUID scheme with a dynamic dimensionality means a GUID scheme where the GUIDs do not all need to have the same number of coordinates.

One of Polymorph's P2P routing algorithms uses a GUID scheme with dynamic dimensionality. In other words, the peers do not have the same bit size GUID. The diagram below shows an example of a P2P network using a multi-dimensional GUID scheme:

![A P2P network using a multi-dimensional GUID space](https://jenkov.com/images/p2p/peer-addressability-2.png) 

## GUIDs as Addresses

The primary function of a GUID is to work as an address. If you know the GUID of the peer you want to communicate with, the P2P network routing algorithm can figure out how to find that peer in the network - even if the first peer doesn't directly know the location (IP address + port) of the peer it wants to communicate with.

## GUIDs as Identifiers

By default a peer GUID denotes an address - a location in the network - but does not guarantee which computer or person that is located at that GUID address. Today it could be one person, tomorrow it could be another person.

GUIDs can be used as identifiers in addition to just addresses. For instance, if the GUID 963 always belong to the same person or computer, then the GUID no longer just tells where a peer is located in the network, but also which identity the GUID represents.

## Splitting Identity from Address

Sometimes a person might want to join a P2P network from different locations. For instance, at home, at work, and when traveling to another country.

For the P2P network to work optimally, the network might prefer to give peers different GUIDs depending on the geographical location of the peer. However, that means that a person joining a P2P network from different geographical locations will have different GUIDs when joining from these different locations. Thus, the GUID can no longer be used as an ID but only as an address.

To solve this a P2P network may split the ID of a user or computer from its address, and assign two different GUIDS to represent the identity and address. Thus, a user can keep the same identity GUID independently of the address GUID the user gets when joining the network (based on geographical location of the user's computer when joining). Thus, a peer might have both an address and an identity GUID (2 in total).

If a P2P network split the identity of a peer from its address then the P2P network may need a function to lookup the address of an identity, so other peers can find out what address to connect to, to contact that the user or computer with that identity.
