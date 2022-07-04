# Software Architecture

[Software Architecture](https://jenkov.com/tutorials/software-architecture/index.html)

Note: This tutorial is still work in progress. It will be updated bit by bit, until it reaches a more comprehensive and coherent state. However, you may still get something out of it already now.

Software architecture and software design are two aspects of the same topic. Both are about how software is structured in order to perform its tasks. The term "software architecture" typically refers to the bigger structures of a software system, whereas "software design" typically refers to the smaller structures.

Exactly where the boundary is between architecture and design is hard to say, since the architecture of a system also affects its design. The design of the bigger structures affect the design of the smaller structures. To set it somewhere meaningful (to decide what should be included and excluded in this tutorial), I have set the boundary at the process level. Software design is thus concerned with the internal design of a single software process, whereas software architecture is concerned with the design of how multiple software processes cooperate to carry out their tasks.

![The boundary between software design and software architecture](https://jenkov.com/images/software-architecture/software-architecture-introduction-1.png)

How does my definition of software architecture fit with the term "distributed systems" ? The way I see it, software architecture provides the basic structures on top of which the various distributed algorithms can run. Yes, there is a certain overlap between the two terms, but various different distributed algorithms can run on top of the same underlying architectures.

Software architecture is also influenced by the hardware architecture of the whole system (software + hardware). You may need different architectures (and thus design) depending on what hardware you are using. Or, you may choose different hardware depending on your architecture.

## Common Software Architectures

There are many different types of architectures, but some architectural patterns occur more commonly than others. Here is a list of common software architecture patterns:

- Single process.
- Client / Server (2 processes collaborating).
- 3 Tier systems (3 processes collaborating in chains).
- N Tier systems (N processes collaborating in chains).
- Service oriented architecture (lots of processes interacting with each other).
- Peer-to-peer architecture (lots of processes interacting without a central server).
- Hybrid architectures - combinations of the above architectures.

Here is a simple illustration of these architectures.

![Software architecture overview.](https://jenkov.com/images/software-architecture/software-architecture-introduction-2.png)

## Process Communication Channels

Processes typically have three media through which they can communicate with each other. These are:

- Network
- Disk
- Pipes

Processes can communicate with each other via computer networks. Through this medium a process can communicate with processes running on the same computer as itself, or with processes running on a different computer, provided that the two computers running the processes are connected with a computer network.

Processes running on the same computer can also communicate with each other via the computer's hard disk (or other disks like USB disks etc.). Processe A can write files to the disk which are processed by Process B. A reply can also be sent back from Process B in a file written to disk which Process A then reads.

Processes can also communicate via network storage, which is essentially a hard disk connected to the computer network. This way processes can also communicate with processes running on different computers, via the combination of network and disk communication.

Depending on the operating system the processes are running on, processes running on the same machine can also communicate with each other through pipes. Pipes are channels of communication provided by the operating systems for processes. The communication takes place like network communication, but the messages exchanged are kept internally in the RAM of the computer. Pipes can be faster than network communication, because a lot of network protocol overhead can be eliminated when the communicating processes run on the same computer.

Processes could also communicate via a RAM disk, which is a virtual hard disk allocated in the RAM of a computer. A RAM disk looks like a disk to the process, but is much faster than a disk because the data is only stored in RAM.

## Process Communication Modes

Processes can communicate with each other in either:

- Synchronous mode.
- Asynchronous mode.

When a process A communicates with a process B synchronously, it means that process A sends a message to process B and waits for B to reply. Process A does not do anything until it gets a reply from process B.

When two processes communicates asynchronously, the processes sends messages to each other without waiting for each other to reply. Process A may send a message to process B and then continue with some other work. At some point process B sends a message back to process A, and process A processes that message when process A has time for it.

Synchronous and asynchronous communication has different advantages and use cases. You can use asynchronous communication to implement synchronous communication, or use synchronous communication to implement asynchronous communication.

The synchronous and asynchronous communication modes are illustrated here:

![Synchronous vs asynchronous communication mode.](https://jenkov.com/images/software-architecture/software-architecture-introduction-3.png)
