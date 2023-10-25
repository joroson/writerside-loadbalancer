# GSLB

Global Server Load Balancing (GSLB) is a technology used to distribute client requests across multiple geographically
dispersed servers in order to optimize resource use, maximize throughput, minimize response time, and avoid overloading
any single server. Unlike traditional load balancing, which operates in a single data center, GSLB works at a global
level, directing client traffic to the nearest or best-performing data center.

## Key Features

1. **Geographic Routing**: GSLB can direct traffic based on geographic locations of the clients and servers.
2. **Fault Tolerance**: GSLB provides a high level of fault tolerance by rerouting traffic in case of local or regional
   server failures.
3. **Application Awareness**: It can take into account the health and performance metrics of individual application
   servers, not just network metrics.
4. **DNS-based Decision Making**: Often GSLB solutions use DNS queries to make intelligent routing decisions.
5. **Data Center Affinity**: GSLB can also ensure that a client's multiple requests go to the same data center for
   session consistency.
6. **Multi-Protocol Support**: While initially designed for HTTP/HTTPS traffic, modern GSLB solutions also support other
   protocols.
7. **Dynamic Weighting**: GSLB solutions can dynamically adjust the weight or priority of a server based on real-time
   conditions, including server load and connection speed.

## Use Cases

1. **Disaster Recovery**: Automatic failover in the event of site failure.
2. **Content Localization**: Serving different content to users based on their geographical location.
3. **Compliance**: Routing traffic to ensure compliance with local laws and regulations.
4. **High Availability**: Distributing traffic to achieve maximum uptime.

In summary, GSLB offers a powerful way to manage global traffic, improve application performance, and increase
availability. It is a critical component in any organization's multi-data center strategy.

### EDNS-CS

EDNS-CS stands for Extension Mechanisms for DNS - Client Subnet. This is an extension to the DNS protocol that allows a
DNS resolver to specify the network subnet for the client making the request, as part of the DNS query. This is
particularly useful in the context of Global Server Load Balancing (GSLB) and Content Delivery Networks (CDNs), where
it's important to route user requests to the geographically closest or most appropriate server.

EDNS-CS aims to improve the routing accuracy by providing more specific information about the client's location.
Normally, the DNS resolver receives the query and passes it on to the authoritative DNS server without any indication of
where the original client is located. With EDNS-CS, the resolver can include part of the client's IP address in the
request, enabling the authoritative server to make a more informed decision on how to route the client to the most
appropriate endpoint.

However, it should be noted that the use of EDNS-CS has been subject to some privacy concerns, as it potentially exposes
more information about the client to the authoritative DNS server.

In summary, EDNS-CS is designed to optimize content delivery and server selection by including client subnet information
in DNS queries.