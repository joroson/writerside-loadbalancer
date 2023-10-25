# Deployment
<show-structure for="chapter,procedure" depth="2"/>

There are a number of ways that HyperBalance can be deployed depending on the needs and requirements of the customer.
Within each of the HyperStore deployment methods are a number of different implementations that can be used to achieve
the results that the customer is looking for.

## Single Cluster

Smaller deployments will only need a single pair of load balancers, they are typically only serving a low number of
nodes.

### Virtual Services (Layer 7 SNAT) {id="sc-vs-l7"}

This method offers the full functionality of the load balancer and is the preferred method of installation where
throughput requirements are satisfied by the appliance connectivity.

### SDNS (Smart DNS) {id="sc-sdns"}

Single clusters that are being deployed with virtualised load balancers will be best served by implementing SDNS. SDNS
is described in greater detail later in this document.

## Multi-cluster multi DC

This method is frequently used with large companies or geographically dispersed entities using Cloudian HyperStore
clusters.

### Virtual Services (Layer 7 SNAT) {id="mc-vs-l7"}

This method offers the full functionality of the load balancer and is the preferred method of installation where
throughput requirements are satisfied by the appliance connectivity.

### Global Server Load Balancing

This method offers the full functionality of the load balancer and is the preferred method of installation where
throughput requirements are satisfied by the appliance connectivity. GSLB provides redundancy by allowing users to
failover to a separate cluster.

#### Weighted Round Robin

Requests are distributed in a round robin fashion based on their individual weightings.

#### Topology Weighted Round Robin

Requests are distributed based on the requester's origin, falling back to round robin in accordance with the weighting
if nothing else matches.

#### Failover Group

Requests are always distributed to the first available member that is passing health checks. This could also be
described as chained failover.

#### SDNS (Smart DNS) {id="mc-sdns"}

In a multi cluster installation that has extremely high throughput requirements and extremely good network performance
which may be limited by even 100GbE an SDNS implementation may be necessary. SDNS is described in greater detail later
in this document.

