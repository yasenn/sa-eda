[Service Oriented Architecture (SOA)](https://jenkov.com/tutorials/soa/soa.html)

Service oriented architecture (SOA) is an architecture where independent systems and applications communicate with each other by exposing and using services. Services are defined using open standards, making inter-communication much easier to implement, and less dependent on proprietary communication protocols.

## From DOA to SOA

SOA follows the idea of a Distributed Object Architecture (DOA) where objects in applications could move around freely between servers and call each other remotely etc. The idea was that an object calling another object should not have to know whether the called object was residing locally, or remotely. This should be transparent to the calling object.

This architecture is slowly being abandoned, as too fine grained distributed object communication is both very complex, and does not perform well.

Distributed objects are complex because there are more error possibilities when calling a remote object, than when calling a local. For instance, you typically need two phase commit transactions to coordinate a distributed transaction, where a single phase transaction may do locally.

Additionally, you had less control over the communication overhead incurred from unnecessary out-of-process communication, and from moving objects between "containers" or "servers" behind your back. Thus application designers wanted to be able to control location of objects, to lower complexity and increase performance.

<table style="padding-bottom:10px;"><tbody><tr><td align="center"><img src="https://jenkov.com/images/web-services/soa-1.png" alt="A distributed object architecture."></td></tr><tr><td align="center"><b>A distributed object architecture.</b></td></tr></tbody></table>

Instead larger grained less mobile services have been introduced - SOA. Service can move, but they typically do not move as dynamically as people imagined distributed objects would. Additionally, when you call a service you are typically aware that you are calling a remote entity. This means that you have better control of both complexity and performance.

<table style="padding-bottom:10px;"><tbody><tr><td align="center"><img src="https://jenkov.com/images/web-services/soa-2.png" alt="A service oriented architecture (SOA)."></td></tr><tr><td align="center"><b>A service oriented architecture.</b></td></tr></tbody></table>

Some people sarcastically say that SOA stands for "Same Old Architecture" - which is actually not that far from the truth. Todays services are strikingly alike yesterdays remote procedure call protocols. The main difference is that today services are more and more communicating via open standards, like SOAP, REST etc. meaning the communication layer becomes easier to implement. SOA is not, however, the big increaser of "Return on Investment" as some authors wants you to believe.

Another difference is that SOA introduces a set of new concepts, and attempts to standardize some existing concepts across the industry. Some of these concepts are:

- Enterprise Service Bus
- Service Composition
- Service Transactions
- Service Repositories
- Service Orchestration

# Services vs. Applications 

[Services vs. Applications](https://jenkov.com/tutorials/soa/services-applications.html)

When you start learning about service oriented architecture you might wonder, what the difference is between a service and an application.

There are no precise definitions of a service or an application. Services and applications are both software programs, but they do tend to have some differing traits. I have summed up the most common traits in the table below:

  

Services often target smaller and more isolated problems than applications. Applications often expose and call services, sometimes services in other applications. It's hard to get more concrete than this. Here is an example of why:

A mail server (as software) can be thought of as both a service and an application. It runs on some server (hardware) somewhere on the network. It exposes 2-3 primary services: An SMTP service used to send email, and a POP3 and an IMAP service to read email via. The mail server may not have a user GUI that the users can interact with. They might just use some standard email clients.

The mail server may had an administrator GUI though. But there is no guarantee. The mail server could also just be configured via configuration files.

The reason I would still call a mail server an application is that it exposes 2-3 services, is intended to be used by end users (though via some client applications), and it targets a whole problem domain. But really, you might as well call it a "mail service". The border between services and applications is unclear.

Here is an illustration of the mail server example:

<table style="padding:10px;"><tbody><tr><td align="center"><img src="https://jenkov.com/images/web-services/soa-services-applications-1.png" alt="A mail server (application) exposing 3 different services."></td></tr><tr><td align="center"><b>A mail server (application) exposing 4 different services.</b></td></tr></tbody></table>


# ESB

[Enterprise Service Bus (ESB)](https://jenkov.com/tutorials/soa/esb.html)

An "Enterprise Service Bus" (ESB) is a system to which all services are connected. Through the enterprise service bus all connected services can also be accessed. Here is an illustration of an enterprise service bus which acts as central "bridge" or "gateway" to all applications exposing services underneath it:

## ESB Basics

The term "bus" is an analogy to the internal bus of a computer onto which the CPU, RAM and other chips are connected. An enterprise service bus is typically implemented as a server or a set of servers, and is thus more than just a "network".

<table style="padding:10px;"><tbody><tr><td align="center"><img src="https://jenkov.com/images/web-services/esb-1.png" alt="An Enterprise Service Bus (ESB)."></td></tr><tr><td align="center"><b>An enterprise service bus with applications (services) connected</b></td></tr></tbody></table>

Clients and services connected to an enterprise service bus do not communicate directly. They communicate via the ESB. This is done by having the ESB essentially expose the same service interface to potential clients, that the connected services expose to the ESB. This indirection via the ESB has some advantages and disadvantages, which I will cover in the rest of this text.

## ESB as Single Point of Access

One advantage of connecting clients and services via an enterprise service bus is that clients need only look for services in a single location: The enterprise service bus. If a service is moved from one server to another, you only need to reconfigure the ESB. The clients still just access the service via the ESB.

## ESB as Transaction Manager

Another advantage is that the ESB can coordinate distributed transactions which multiple services participate in. When multiple distributed services need to participate in a transaction some entity typically has to coordinate the transaction. Rather than forcing the client to do this, the enterprise service bus can do so. The client may still have to demarcate the beginning and end of the transaction, even if the work of coordinating the participants is done by the ESB.

<table style="padding:10px;"><tbody><tr><td align="center"><img src="https://jenkov.com/images/web-services/esb-2.png" alt="An Enterprise Service Bus (ESB) as transaction manager."></td></tr><tr><td align="center"><b>An enterprise service bus (ESB) managing a transaction spanning three services</b></td></tr></tbody></table>

## ESB as Security Manager

Security aspects like authentication and authorization can be centralized in the enterprise service bus. Even if a service in an application does not have authentication and authorization, the enterprise service bus can require this in the service interface it exposes to potential clients.

<table style="padding:10px;"><tbody><tr><td align="center"><img src="https://jenkov.com/images/web-services/esb-3.png" alt="An Enterprise Service Bus (ESB) as security manager."></td></tr><tr><td align="center"><b>An enterprise service bus (ESB) authenticating and authorizing the client before forwarding service requests to services.</b></td></tr></tbody></table>

## ESB as Service Proxy

An ESB may function as a gateway or proxy for appliations that do not expose a standardized service interface to the world. For instance, lets say an application exposes a Java RMI service. The rest of your network is running on .NET which cannot directly call the RMI service.

To solve this problem you can implement a service proxy in Java which can call the RMI service. The service proxy then exposes a web service interface (SOAP + WSDL) via the ESB to the .NET applications.

Such a proxy service does not have to be a built-in capability of an ESB. It can also just be deployed as a separate service, made available via the ESB.

<table style="padding:10px;"><tbody><tr><td align="center"><img src="https://jenkov.com/images/web-services/esb-4.png" alt="An Enterprise Service Bus (ESB) as service proxy."></td></tr><tr><td align="center"><b>An enterprise service bus (ESB) as service proxy for a service with a proprietary protocol.</b></td></tr></tbody></table>

## ESB as Gateway to the World

If some clients need to connect to services running in the outside world, the ESB can potentially function as a gateway to the world outside. Again, security aspects etc. can be added ontop of the external service. Furthermore, if the external service is capable of participating in distributed transactions, the ESB can coordinate this too.

<table style="padding:10px;"><tbody><tr><td align="center"><img src="https://jenkov.com/images/web-services/esb-5.png" alt="An Enterprise Service Bus (ESB) as gateway to the world."></td></tr><tr><td align="center"><b>An enterprise service bus (ESB) as gateway to the world.</b></td></tr></tbody></table>

## ESB Disadvantages

Connecting your services via an ESB also has a few disadvantages. First of all the ESB may become a single point of failure. If the ESB is down, no communication between clients and services can take place. Second, the extra level of indirection may result in decreased performance of client-service communication.

# Service Composition

[Service Composition](https://jenkov.com/tutorials/soa/service-composition.html)

Service composition means composing a larger service by combining many smaller services. This is the same principle used when composing a larger software component from many smaller components. Here is a diagram illustrating service composition:

<table style="padding:10px;"><tbody><tr><td align="center"><img src="https://jenkov.com/images/web-services/composition-1.png" alt="Service Composition"></td></tr><tr><td align="center"><b>Service Composition - composing a service by combining several smaller ones.</b></td></tr></tbody></table>

## Service Composition Performance

While service composition may look compelling on paper, just like component composition would, keep in mind that services typically communicate with each other via the network. That means that inter-service communication is much slower than typical inter-component communication, which typically takes place inside the same address space (application / process). Decomposing your larger services into too many smaller services may hurt performance. Especially if the services communicate internally via an enterprise service bus (ESB).

# Service Reusability 

[Service Reusability](https://jenkov.com/tutorials/soa/service-reusability.html)

The reusability of a service depends a lot on its design and purpose. By "reusability" is meant in how applications or larger services, can a given smaller service be reused. I'll explain this with a small example:

Imagine you have two applications, A and B, that both need customer information. Application A only needs the customers first name and last name, but application B needs the customers first name, last name, customer number, phone number, email address etc. The requirements are summarized here:

Application A
\-\-\-\-\-\-\-\-\-\-\-\-\-\-
 \- First Name
 \- Last Name

    
Application B
\-\-\-\-\-\-\-\-\-\-\-\-\-\-
 \- First Name
 \- Last Name
 \- Customer Number
 \- Phone Number
 \- Email Address
 \- etc.

In order to service both application A and B you have two options:

1. Create one big Customer Service which returns all customer information
2. Create two Customer Services. One that returns all customer information, and one that only returns first name and last name.

From a service reusability perspective it would of course be nice to only have one customer service to develop and maintain. This service could then be reused in both appliation A and B.

From a performance perspective though, the one big customer service would impose an overhead on the communication when used by application A (which only needs first name and last name), because the big customer service sends back more data than application A needs.

The design choice between one wide service or multiple tailored services is illustrated here:


# Service Transactions

[Service Transactions](https://jenkov.com/tutorials/soa/service-transactions.html)

Once in a while services need to participate in transactions. This is done to make sure that the business logic is carried out correctly, or completely canceled in case one of the services fail. Let's look at a classic example:

A bank application needs to transfer money from one account to another. Currently the bank system has two services:

- Deposit Service
- Withdrawal Service

Here is an illustration of the bank system:

<table style="padding:10px;"><tbody><tr><td align="center"><img src="https://jenkov.com/images/web-services/transactions-1.png" alt="Service Transactions - a simple bank application using two services"></td></tr><tr><td align="center"><b>Service Transactions - a simple bank application using two services.</b></td></tr></tbody></table>

In order to transfer money from one account to another, the bank application needs to call the withdrawal service and deposit service. For instance, first withdraw $100 from account A, and then deposit the $100 in account B.

If for some reason one of the two service calls fails, then the bank system will end up in an inconsistent state. If the bank system called the withdrawal service first and the deposit service call fails, then $100 will have been withdrawn without them being deposited anywhere. $100 were lost in cyberspace. If, on the other hand, the deposit service was called first and then the withdrawal service fails, then $100 will have been deposited without being withdrawn from any account. $100 was created out of thin air.

The solution to this problem is to have the withdrawal and deposit service calls be executed as a single, atomic action. This is what transactions are for.

## Transactions as Atomic Actions

A transaction groups one or more actions together, and makes sure they are executed as if it was just a single action. If one of the actions fail, all of the actions fail. Only if all actions succeed will the result of the actions be "committed" (permanently stored) to the system.

Here is an illustration of the withdrawal and deposit service being grouped into a transaction:

<table style="padding:10px;"><tbody><tr><td align="center"><img src="https://jenkov.com/images/web-services/transactions-2.png" alt="Service Transactions - two services grouped into a single transaction"></td></tr><tr><td align="center"><b>Service Transactions - two services grouped into a single transaction.</b></td></tr></tbody></table>

## Two Phase Commit Transactions

Services participating in a transaction needs to be coordinated in order to assure that either all or non of the services called "commit" their actions within that transaction. A popular way to coordinate such distributed transactions is the "Two Phase Commit" protocol.

The two phase commit protocol consists of three steps:

1. Begin Transaction
2. Prepare Phase
3. Commit Phase

First all participants are told to participate in a transaction. From this point on, all actions carried out by each participant refering to this transaction, must be carried out as a single action (all or non). The actions cannot be committed to the main system yet, but must be kept internally in the participant (service), until the participant is instructed to commit the actions.

Second, once all actions are executed successfully by all participants, all participants (e.g. services) are ordered to move to the "prepare phase". Once a participant is successfully in prepare phase, the participant must guarantee that all actions carried out inside the transaction are ready to be committed. If the participant fails after it has successfully moved into the prepare phase, it must be able to commit the actions once the participant is functioning correctly again. In other words, the actions executed inside the transaction must be able to survive even a participant crash / reboot. This is usually done by writing a transaction log to a durable medium , e.g a hard disk.

If one of the participants cannot move to the prepare phase, all participants are ordered to rollback (abort) the transaction.

If all participants successfully move to the prepare phase, then all participants are now ordered to commit their actions. Once committed, the actions are then visible in the system, and permently executed.

### A Two Phase Commit Weakness

The two phase commit protocol is not 100% secure. Imagine if a service crashes after entering the prepare phase. Now all services are requested to commit. Imagine that the failed service is the last service in the chain to be ordered to commit. But the commit order fails, because the service has crashed. All other services in this transaction would already have committed their actions, but not this last one.

Normally, the service would have to commit it's part of the transaction once the service is operational again. However, if the service never comes back up, then what? It's actions has not been committed, what is the status of the system then?

Here is an illustration of a two phase commit transaction where the last service fails to commit:

<table style="padding:10px;"><tbody><tr><td align="center"><img src="https://jenkov.com/images/web-services/transactions-3.png" alt="Service Transactions - A two phase commit transaction failing"></td></tr><tr><td align="center"><b>Service Transactions - A two phase commit transaction failing.</b></td></tr></tbody></table>

## Transaction Coordination

When multiple services are to participate in a transaction, some entity must coordinate the transaction. In other words someone has to say when the transaction begins, and when to move to the prepare and commit phases. This entity, the transaction coordinator, can be either:

- The application
- An [enterprise service bus](https://jenkov.com/tutorials/soa/esb.html)
- A separate transaction manager / service

In the example earlier in this text the application coordinated the transaction.

## One Service Per Transaction

A way to simplify transaction management in a service oriented architecture is to design the services so each transaction is contained within a single service. For instance, in the example at the beginning of this text the money transfer would be implemented as a separate service, instead of a transaction involving two services. Here is how that would look:

<table style="padding:10px;"><tbody><tr><td align="center"><img src="https://jenkov.com/images/web-services/transactions-4.png" alt="Service Transactions - Each transaction is contained within its own service"></td></tr><tr><td align="center"><b>Service Transactions - Each transaction is contained within its own service</b></td></tr></tbody></table>

# Service Repositories 
[Service Repositories](https://jenkov.com/tutorials/soa/service-repositories.html)

A service repository is a catalogue in which you can see what services are available on a network. For instance, imagine you have a service oriented architecture in a bank. In the beginning when the number of services is low it might be possible to keep track of what services are running where in spreadsheets etc. But when the number of services grow, this method may not continue to be suitable.

Instead of keeping track of services manually, you can register the services in a service repository. To find out what services are available on the network you query the service repository. This can be done via a standardized interface, meaning computerized clients can do this. It does not have to be done by a human. The following diagrams illustrates this:

<table style="padding:10px;"><tbody><tr><td align="center"><img src="https://jenkov.com/images/web-services/repositories-1.png" alt="Service Repositories - A client looks up a service location in a repository, and calls the service afterwards."></td></tr><tr><td align="center"><b>A client looks up a service location in a repository, and calls the service afterwards.</b></td></tr></tbody></table>

Several service oriented technologies have a service repository mechanism. For instance, in the web service world you have UDDI repositories, and in Jini you have a service registry.

## Easier Service Relocation

If clients lookup the services they need via a service repository, relocating a service becomes easier. You just update the service repository with the new location of the service, and instruct all clients to lookup the service location again (e.g. by simply restarting each client application). This is somewhat easier than having to update the configuration of each client with the new network location of the relocated service.

# SOA - Service Proxy

[SOA - Service Proxy](https://jenkov.com/tutorials/soa/service-proxy.html)

A service proxy is a service which translates service calls betweeen two different client-service protocols. This may sound a bit abstract, so here is an example:

Imagine you have a service that is only accessible via Java's RMI (Remote Method Invocation). You need to access this service via a web service (SOAP) interface, because the rest of your service oriented architecture is standardized on SOAP.

To solve this problem you can implement a service proxy which receives SOAP calls and translates them into their corresponding RMI calls to the Java RMI service.

Here is an illustration showing a client calling a service proxy via SOAP. The service proxy then calls the Java RMI service. The response from the Java RMI service is translated into SOAP by the service proxy, and returned to the client.

<table style="padding:10px;"><tbody><tr><td align="center"><img src="https://jenkov.com/images/web-services/soa-3.png" alt="Service Proxy - a service that translates from one service protocol to another."></td></tr><tr><td align="center"><b>A service proxy that translates between SOAP and Java RMI.</b></td></tr></tbody></table>

## The ESB as Service Proxy

Some [Enterprise Service Bus (ESB)](https://jenkov.com/tutorials/soa/esb.html) products have built-in service proxy capabilities. Using an ESB with service proxy capabilities makes it a lot easier to "glue together" (integrate) your various different systems in your service oriented architecture.
