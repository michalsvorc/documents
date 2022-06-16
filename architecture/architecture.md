# Architecture

## TCP, UDP, TLS

- [User Datagram Protocol (UDP) - Wiki](https://en.wikipedia.org/wiki/User_Datagram_Protocol)
- [Transmission Control Protocol (TCP) - Wiki](https://en.wikipedia.org/wiki/Transmission_Control_Protocol)
- [Comparison of UDP and TCP](https://en.wikipedia.org/wiki/User_Datagram_Protocol#Comparison_of_UDP_and_TCP)

The TCP/IP protocol is a set of protocols, which includes many protocols, and TCP, UDP, TLS, etc. are just among them.

TLS, Transport Layer Security, is a security layer which sits on top of a transport layer such as TCP and allows secure
communication over an insecure network. TLS encrypts data before it reaches TCP (or other transports), and decrypts it
after being handed over by the transport at the other end. It also handles the necessary key exchange.

## Bandwidth

- [Wikipedia](<https://en.wikipedia.org/wiki/Bandwidth_(computing)>)

Bandwidth is the maximum rate of data transfer across a given path. Bandwidth may be characterized as network bandwidth
data bandwidth or digital bandwidth.

## Load balancing

- [Wikipedia](<https://en.wikipedia.org/wiki/Load_balancing_(computing)>)

Load balancing refers to the process of distributing a set of tasks over a set of resources (computing units), with the
aim of making their overall processing more efficient. Load balancing can optimize the response time and avoid unevenly
overloading some compute nodes while other compute nodes are left idle.

It will also do the regular health checks to your instances and it will know when to send the load on the instances.

Alternatives to load balancing include scaling vertically. To implement fail-over you typically need to have your data
replicated across multiple machines.

Types:

- Round Robin: does not take server load into consideration, it distributes incoming requests equally among backend
  servers.
- Least Connection
- Least Response
- Least Bandwidth

## Redundancy

Redundancy is the duplication of critical components or functions of a system with the intention of increasing
reliability of the system, usually in the form of a backup or fail-safe, or to improve actual system performance.

## Failover

Failover is not the same as Load Balancing.

The goal of fail-over is to allow work that would normally be done by one server to be done by another server should the
regular one fail.

## Scalability

Scalability means that an application can handle greater loads by adapting some techniques.

- Vertical scalability means increasing the size of the instance.
- Horizontal Scalability means increasing the number of instances for your application.

High availability means running your application in at least 2 data centers (Availability Zones).

## Cache

- [Caching Strategies - codeahoy.com](https://codeahoy.com/2017/08/11/caching-strategies-and-how-to-choose-the-right-one/)

Caching strategies:

- Cache-Aside
- Read-Through Cache
- Write-Through Cache
- Write-Around

Eviction strategies:

- Least Recently Used (LRU): The oldest element is the Less Recently Used (LRU) element. The last used timestamp is
  updated when an element is put into the cache or an element is retrieved from the cache with a get call.
- Least Frequently Used (LFU): For each get call on the element the number of hits is updated. When a put call is made
  for a new element (and assuming that the max limit is reached) the element with least number of hits, the Least
  Frequently Used element, is evicted.
- First In First Out (FIFO): Elements are evicted in the same order as they come in. When a put call is made for a new
  element (and assuming that the max limit is reached for the memory store) the element that was placed first (First-In)
  in the store is the candidate for eviction (First-Out).
- Shortest TTL: The cache evicts the keys with the shortest TTL set.
