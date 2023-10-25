# GSLB

## Why is GSLB needed?

- Global Presence
- High(er) Availability
- Disaster Recovery
- Load Distribution
- Reduced Latency
- Data Sovereignty

### Global Presence

The modern world is much more global than it used to be. Faster internetwork connectivity allows for geographically
dispersed data centres to work as one and to provide redundancy for each other. GSLB can be used to route traffic to any
available location.

### High(er) Availability

oad balancing provides high availability within a data centre or location. GSLB is able to load balance load balancers,
that means that it is providing high availability of your high availability services. If a data centre goes offline due
to a network outage or a maintenance event your user's traffic will still be served.

### Disaster Recovery

Provided by the additional high availability is the possibility of immediate DR instigation. With GSLB configured to
provide failover in the event of primary data centre failure, business continuity can be provided seamlessly to end
users.

### Load Distribution

GSLB can implement topologies to distribute traffic based on pre-defined rules. For example requests from UK users are
always sent to UK data centres unless there is a failure, in that case they will be served by another data centre.

### Reduced Latency

GSLB can implement topologies don't just need to be used to for localisation. Sending traffic to the nearest data centre
by default also improves latency therefore improving responsiveness.

### Data Sovereignty

Finally, and something that is becoming much more important to the world is the idea of data sovereignty. There are
quite a few countries now that have legal requirements mandating that data must reside in a specific geographical
region. GSLB can be used to ensure that data stays where it should whilst still being accessible by those that need it.

<procedure title="GSLB Process" id="gslb-process">
   <p>A client performs a DNS lookup against an FQDN</p>
   <step>The lookup is sent to the default network infrastructure</step>
   <step>The DNS server sends the request on to the GSLBs on the load balancer appliances.</step>
   <step>The GSLB responds to the request based on the configuration that it holds and returns a record.</step>
   <step>The DNS server receives the response and then passes it back to the client.</step>
   <step>The client is now able to send their request to the IP address provided by the GSLB.</step>
   <p></p>
</procedure>

