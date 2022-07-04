# Peer-to-Peer (P2P) Networks via jenkov.com

[Peer-to-Peer (P2P) Networks](https://jenkov.com/tutorials/p2p/index.html)

_Peer-to-Peer_ (_P2P_) networks is a class of distributed systems in which peers (computers or "nodes") work together without a central server to both provide and use one or more services. Thus, in a peer-to-peer network the peers typically acts as both clients and servers - meaning clients of other peers, and servers for other peers. This is the reason the nodes in a peer-to-peer network are referred to as _peers_ \- because the nodes are each other's equals (peers), - unlike in a client-server topology where the client and server have different roles and responsibilities.

_P2P networks_ are also [decentralized systems](https://jenkov.com/tutorials/decentralized-systems/index.html). However, not all decentralized systems are _P2P_ systems. For instance, a database such as Cassandra may use P2P techniques internally, where all nodes in a Cassandra cluster are both clients and servers of each other. However, a Cassandra cluster will also have a set of external clients which are only clients of the cluster, and not participants in providing the database service. Thus, a system of clients using a Cassandra database is not classified as a P2P network. However, P2P techniques can still be very useful within such systems.

## In P2P, the Network is the Service

In a normal client / server application, the server typically provides a service to the client, which is said to "consume" the service. In a P2P network however, each peer both provides and consumes the service. You could be tempted to say, that " The Network is the Service".

## Global Scale P2P Networks

In this tutorial I will focus on global scale P2P networks - on how to get millions of peers to work together, without a central server. Global scale P2P networks can typically also be used for smaller workgroups, but small workgroup P2P technologies are not always good for global scale P2P networking. That's why I focus on large scale P2P technologies.

## Existing P2P Networks and P2P Technologies

There are already many active P2P networks out there, and several P2P technologies. Some of the products that are centered around a P2P network are:

- LBRY
- IPFS
- Beaker Browser
- Skype
- BitTorrent
- Gnutella

There is also an open source toolkit named libp2p which provides some implementations of the Kademlia P2P algorithm.

## P2P Network Algorithms

By the term _P2P network algorithm_ I mean the core algorithms around how peers in a P2P network connect to each other, find each other and route messages between each other, as described in the section [P2P Network Challenges](https://jenkov.com/tutorials/p2p/index.html#p2p-network-challenges) below.

P2P network algorithms are typically centered around a specific P2P topology. These P2P topogolies can basically be categorized into two classes of P2P networks:

- Structured P2P Topologies
- Unstructured P2P Topologies

I will explain both in a bit more detail in the following sections.

### Structured P2P Topologies

Structured P2P topologies attempt to organize all peers in the network into a single, structured topology. This structured topology then provides reasonably predictable findability of peers and routability of messages. Structured P2P topologies attempt to avoid network fragmentation too.

Some of the structured P2P network algorithms I know of, are:

- [Chord](https://jenkov.com/tutorials/p2p/chord.html)
- Kademlia
- Tapestry
- Pastry
- Polymorph Polyring (see more later)

All of these P2P algorithms are similar. They all organize the peers into a single virtual ring with each peer holding a routing table pointing to a subset of the other peers in the network. In other words, all peers are part of the same ring. The main difference between each peer in the ring is which other peers it references in its routing table.

Chord and Kademlia use similar types of routing tables and algorithms. Also, Pastry and Tapestry use similar types of routing tables. More specifically, Pastry and Tapestry use a routing table design where you can adjust the number of peers kept in each peer's routing table. The more peers in a routing table, the less hubs it takes to find a specific peer, but the more memory / storage is needed to keep the routing table within each peer.

Other algorithms can be layered on top of the fundamental connection, location and routing algorithms. Algorithms such as distributed consensus, distributed hashtables (DHT), broadcast, multicast, caching etc. However, in this P2P tutorial I will focus mostly on the underlying P2P network organizing algorithms.

### Unstructured P2P Topologies

Unstructured P2P topologies do not attempt to organize all peers into a single, structured topology. Rather, each peer attempts to keep a "sensible" set of other peers in its routing table - which may work reasonably well for peer findability and message routing, but which does not provide any guarantees. In theory, an unstructured P2P network could fragment into multiple separate networks, thus making findability and routability in the total network impossible.

Some of commonly known unstructured P2P network topologies are:

- Gnutella
- Dandelion
- Dandelion++
- Swim

## P2P Network Algorithms in Polymorph

I am currently working on an "art" project called [Polymorph](https://plmph.com) which which can also be used to implement P2P networks (among other network topologies). Here is my article about the [Polymorph P2P topology and algorithm](https://jenkov.com/tutorials/p2p/polymorph.html).

The Polymorph network topology is designed to enable greater control over network topology and performance than Chord, Kademlia, Pastry and Tapestry. Instead of striving for a uniform topology like Chord, Kademlia, Pastry and Tapestry does, Polymorph strives to enable polymorphic topology, meaning different topologies for different purposes.

The purpose of Polymorph is to create a smart media platform intended to ease the packaging, distribution and consumption of more standard types of media such as text documents, images, animations, video, audio, presentations etc. The P2P network algorithms target the information distribution part of that.

I call Polymorph an "art" project because it is not a project intended to be a fast growing startup. My primary goal with project Polymorph is to see if my ideas actually work in practice - and if yes, to see how well they work.

Even if the ideas in Polymorph work well, there is no guarantee that anyone will actually use Polymorph in practice. Even if some people use it in practice, there is no guarantee they would be willing to pay to use any parts of it. But adoption and monetization is not the main goal of Polymorph. Proof of concept is the main goal. Anything beyond that is "nice-to-have".

Project Polymorph was started in 2021 - in my spare time. Please be patient, as it takes a long time to both design, verify, make a proof-of-concept implementation and document the whole project.

## P2P Network Challenges

A P2P network has to solve a set of challenges in order to be functional. The exact challenges depends on what service the P2P network is trying to provide. However, there are some basic challenges all P2P networks need to address. These challenges are:

- Connectivity
- Addressability
- Findability and / or Routability

Each of these challenges are explained in more detail below. Once each of these challenge have been addressed you can start building a service on top of the P2P network. Depending on the service, other challenges may then emerge, such as:

- Broadcast and multicast
- Caching
- Lookup (DHT)
- Load balancing
- Authentication and authorization
- Privacy
- etc.

My project Polymorph will eventually have to address several of these challenges too.

### Connectivity

For peers in a P2P network to be able to communicate, they must be able to connect to each other. As many peers will be running behind NAT or firewalls, a P2P network must provide some solution to make it possible to still communicate with these peers behind NAT / firewall.

I cover peer connectivity in a bit more detail in this article: [Peer Connectivity](https://jenkov.com/tutorials/p2p/peer-connectivity.html).

### Addressability

For peers in a P2P network to be able to communicate they must also be able to address each other uniquely. Otherwise, a peer cannot specify which peer it wants to talk to. P2P networks typically address this through a peer address or GUID which is unique to each peer.

I cover peer addressability in more detail in this article: [Peer Addressability](https://jenkov.com/tutorials/p2p/peer-addressability.html)

### Findability and Routability

Once a peer has and address of a peer it wants to communicate with, it needs to be able to find that peer in the network so it can establish a connection to it. Alternatively the peer needs to be able to have messages routed through the P2P network to the destination peer.

Typically, P2P networks address these challenges via a combination of the peer addresses (GUIDs) and routing tables. The GUIDs are structured in a way that enables some system of organization of the GUIDs which then enables findability of peers and routability of messages. Therefore you will often see a close connection between the structure of peer GUIDs and the structure of the routing tables used to organize the network and provide findability and routability.

I cover peer findability and message routability in this article: [Peer findability and message routability](https://jenkov.com/tutorials/p2p/peer-findability-and-message-routablity.html)

## P2P Tutorial Video

Some years ago I created a video explaining the basics of how P2P network algorithms such as Chord and Kademlia works. Here it is:

[![P2P Tutorial Video](https://jenkov.com/images/p2p/p2p-video-screenshot.png)](https://www.youtube.com/watch?v=kXyVqk3EbwE "P2P Tutorial Video")

I will probably make a new set of videos for P2P network algorithms as I am updating this tutorial series (from 2021 and forward
