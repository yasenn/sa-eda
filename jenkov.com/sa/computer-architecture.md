# Computer Architecture via jenkov.com

[Computer Architecture](https://jenkov.com/tutorials/software-architecture/computer-architecture.html)

## Computer Architecture Overview

The architecture of computers influences software architecture. In fact, since computers are part of software architecture, computer architecture is part of software architecture too. Your software architecture sits on top of your computer architecture. Therefore I have added this quick overview of computer architecture to this software architecture tutorial.

Here is a diagram illustrating the main components of a computer:

![The main components of a computer](https://jenkov.com/images/software-architecture/computer-architecture-1.png)

The CPU executes the instructions. The RAM stores the instructions and data the instructions work on. The disk drives can store data persistently between system restarts, whereas the RAM is typically deleted when the computer restarts. The NIC connects the computer to a network so it can communicate with other computers. The Bus connects the CPU with the RAM, disk drives and the NIC so they can exchange data and instructions.

I will get into a bit more detail about each of these components in the following sections.

## CPU

The CPU (Central Processing Unit) is what executes all the instructions. The faster the CPU is, the the faster the computer can execute instructions.

Some CPUs have multiple cores. Each core functions like a separate CPU which can execute instructions independently, regardless of what the other cores are doing. If your computer CPU has multiple cores, you should think about how to utilize all the cores when designing your software architecture.

CPUs often have a limited amount of cache memory, which is memory only the CPU can access, and which is much faster than the ordinary RAM.

## RAM

The RAM (Random Access Memory) can store both instructions for the CPU to execute, and the data these instructions are processing. The more memory a computer has, the more data and instructions it can store. The RAM is normally cleared when the computer is shut down or rebooted. It is typically not a permanent storage (although persistent RAM actually exists).

Having a lot of memory in a computer is useful when [caching data](https://jenkov.com/tutorials/software-architecture/caching-techniques.html) which normally reside on disk, or which is read from a remote system via the network (using the NIC).

The speed of the memory determines how fast you can read and write data in it. The faster the better.

## Disk Drives

The disk drives can store data just like the RAM, but unlike the RAM the data is saved even when the computer shuts down. The disk drives are often much slower than RAM to access, so if you need to process big amounts of data, it is preferable to keep that data in RAM.

The speed of the disk drives determine how fast you can read and write data from and to it. The faster the better. The speed of a disk consists of two numbers: Search time and transfer time. Search time tells how fast the disk can search to a certain position on the disk. The transfer time tells how fast the disk can transfer data once it is in the right position.

Some disks have a bit of read cache RAM to speed up reading of data from the disk. When a chunk of data is requested from the disk, the disk will read a bigger chunk into the cache, hoping that the next chunk requested will be within the data stored in the disk cache memory.

Some types of hard disks work more like memory. Among these are SSDs (Solid State Disks). Since SSDs work like memory, the search time is very low. Every memory cell can be addressed directly. This is great if your software is doing many small reads from different places on the disk. The transfer time of SSDs are typically also higher than from normal hard disks.

## NIC

The NIC (Network Interface Card) connects the computer to a network. This enables the computer to communicate with other computers, for instance via the internet. The speed of the NIC determines how fast the computer can communicate with other computers. Of course, the speed of the NIC in the other computers and the network equipment between them matters too.

## The Bus

The Bus connects the CPU to the RAM, disk drives and NIC. The speed of the us impacts how fast the components can exchange data and instructions. Of course the speed of the components themselves impact this too.

## Other Devices

I have left out devices like keyboard, mouse, monitor, USB devices, sound card and graphics cards etc. These typically do not have the big impact on your software architecture (unless you are doing computer games or something similar to that).
