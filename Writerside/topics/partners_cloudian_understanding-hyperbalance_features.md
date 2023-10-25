# Features
<show-structure for="chapter,procedure" depth="2"/>

## Currently Supported

### Layer 7 TCP & HTTP Load Balancing

Load balancing is the primary function of HyperBalance. As such, a wide range of Layer 7 TCP and HTTP load balancing
options are available for use. Configuration guides are available for generic installations. When custom configurations
are required these can be achieved where requirements are within the capabilities of HyperBalance.

### Global Server Load Balancing (GSLB)

GSLB is fully supported and functional at this time, it is bundled with the OEM version of HyperBalance and can be used
by HyperBalance customers. GSLB allows users to failover to an entirely different HyperStore cluster if their
preferred/configured cluster is unavailable or unreachable. GSLB can be configured in the following distribution
methodologies:

#### fogroup (Failover group)

Always prefer one HyperStore Cluster and failover to another Cluster if the preferred Cluster is offline.

#### wrr (Weighted Round Robin)

Distribute requests evenly between the configured Clusters.

#### twrr (Topology Weighted Round Robin)

Distribute requests based on where the requests are coming in from. For example, you can configure the GSLB to always
send users to their closest HyperStore Cluster based on the IP address that they are trying to connect from.

### Smart DNS

SmartDNS (alternatively referred to as GSLB direct-to-node) leverages the functionality of the GSLB to perform health
checks against HyperStore nodes. Nodes that pass health checks are included in the rotation of servers that are
available to service requests made to the HyperStore cluster. SmartDNS is useful for smoothing out utilisation in
Clusters with high node counts.

## Roadmap features

### Scheduled for 8.11

#### GSLB with EDNS Client Subnet

GSLB with EDNS Client Subnet (EDNS-CS) will extend the functionality of the GSLB and SDNS. Currently, topology-weighted
round-robin requires a DNS server at each data centre to work correctly. EDNS CS adds the originating client subnet to
the request and does not require a DNS server at each data centre. This greatly improves the granularity of the topology
tables.

#### GSLB TTL 0

Currently, the minimum value for the global name TTL is 1. For massively concurrent and scheduled tasks a TTL of 1 can
lead to saturation of a particular node. TTL 0 should overcome this issue and distribute requests from extremely bursty
traffic.

### Future release

#### GSLB and SDNS (Smart DNS) dynamic weighting

The ability to dynamically change the weight given to nodes within a HyperStore cluster. This feature will further
smooth cluster utilisation allowing the system to send more requests to under utilised nodes and fewer requests to
over-utilized ones. Values can be calculated and customised based on metrics exposed through health checks performed
against the nodes. This functionality will be available once a suitable metric can be determined and then exposed on the
HyperStore Nodes.
