# Peer Connectivity via jenkov.com

[Peer Connectivity](https://jenkov.com/tutorials/p2p/peer-connectivity.html)

Peers that want to form a peer-to-peer (P2P) network need to be able to communicate with each other. In order to communicate with each other the peers need to be able to connect to each other over the Internet.

If peers are running on a computer located behind a router doing NAT, or behind a firewall, they may not be able connect directly to each other. A peer behind NAT or firewall can typically connect out to the Internet, but cannot receive connections in through the NAT router or firewall (unless explicitly configured to allow inbound connections).

![Peers needing to connect.](https://jenkov.com/images/p2p/peer-connectivity-1.png) 

## Public Peers

A common solution to the problem with peers located behind NAT or firewall starts with detecting those of the peers in the network that are not behind NAT of firewall. Some P2P systems call them _super nodes_. I call these nodes _public nodes_ because they are accessible to other peers in the network. They are "public" so to speak. The peers behind NAT of firewall I call "private" peers.

The second step in the solution is to have the private peers connect to the public peers. This way, private peers can communicate directly with the public peers, and indirectly with other private peers via the public peers.

![Private peers communicating with, and via, public peers.](https://jenkov.com/images/p2p/peer-connectivity-2.png) 

## Hosted Public Peers

It can lead to a bad user experience if a P2P network fully depends on public peers provided by the users themselves. The challenge is, that you cannot control how many users that are public - meaning how many users that join the network that are not behind NAT or firewall. If the network only contains a few public nodes, these public nodes becomes bottlenecks - congestion points, in other words.

A solution to this problem is for the creator of a P2P application to host a certain amount of public peers themselves, to make sure there are enough to provide a good user experience. Granted, this means that the system does not fully depend on the user bandwidth and CPU, but if the alternative is that the P2P app feels slow and laggy, it may be worth it to host a number of public nodes yourself.
