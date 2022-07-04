# Peer Findability and Message Routability via jenkov.com

[Peer Findability and Message Routability](https://jenkov.com/tutorials/p2p/peer-findability-and-message-routability.html)

When a peer-to-peer (P2P) network is small, meaning it has below a certain number of peers in the network, all the peers can know about each other without problems. In other words, all peers in the P2P network can have each other in their routing tables.

However, once a peer-to-peer network grows beyond a certain size - a certain number of peers in the network - it is no longer feasible for each peer to know all other peers in the network. The routing tables of each peer would grow very large, and the amount of communication needed between all the peers to keep the routing tables up-to-date would grow quite large.

## Peer Findability

In a large P2P network, too big for all peers to know about each other, there is still a need for each peer to be able to find other peers connected to the network. By "finding" I mean being able to find their IP address, or the IP address of the public peer the peer is connected to, if the peer is private (behind NAT or firewall). Thus, a P2P network algorithm needs to address _peer findability_.

Typically, P2P network algorithms solve this problem via the design of the routing tables of each peer. The routing tables will organize the peers it knows according to their peer GUIDs in a way that assigns a virtual location to each GUID and thus its corresponding peer. Peers will then contact peers closer and closer to the peer it is looking for, each time asking for the closest peer to the peer it is looking for. For example:

If Peer 1 wants to find Peer 15, Peer 1 will look into its own routing table and find the closest peer in there. Imagine that is Peer 5. Peer 1 then connects to Peer 5 and ask it which peer it knows that is closest to Peer 15. The closest peer to Peer 15 that Peer 5 knows could be Peer 8. Peer 1 then connects to Peer 8 and asks for the closest peer to Peer 15. Peer 8 might know Peer 12. Then Peer 1 contacts Peer 12 and asks for the closest peer to Peer 15. Peer 12 might know Peer 15 and thus returns the information (IP + port) it has on Peer 15 to Peer 1. This process is illustrated below:

![A peer searching for another peer by asking peers closer and closer to the sought peer.](https://jenkov.com/images/p2p/peer-findability-1.png) 

## Message Routability

Some P2P networks may choose not to require direct connections between communicating peers, but instead route the messages between the peers via the P2P network itself. If Peer 1 wants to send a message to Peer 15, first the message might be routed to Peer 5, then to Peer 8, then to Peer 12 and then to Peer 15. Here is how that would look:

![A peer sending a message which is routed by the network to the destination peer.](https://jenkov.com/images/p2p/message-routability-1.png) 

## Implementations are P2P Network Algorithm Specific

The exact peer finding and message routing scheme used by a P2P network depends on the concrete P2P network algorithm. However, most of them will use something similar to what I have outlined above.
