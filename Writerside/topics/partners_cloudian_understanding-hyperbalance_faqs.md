# FAQs

{style="full" collapsible="true"}
Can the customer use their own server hardware for a HyperBalance install?
: The customer should only be using their own server hardware for a HyperBalance when that is the only possible way of
proceeding with a HyperBalance sale. The server hardware must meet or exceed the minimum hardware specification
provided. Cloudian Professional Services will complete the installation on the server.

48 Gbps, does that mean 48 Gbps in + 48 Gbps out? Or is it effectively 24 Gbps when the entire traffic goes through the
LB?
: We are working on some documentation to help with these kinds of questions. When we consider a traffic flow it is
48Gbps in and 48Gbps out from the perspective of the load balancer. As we are a proxy, we are in the path of the traffic
so a unidirectional flow would be 48Gbps in and out, per your example. This does not mean that if you had two concurrent
flows operating bidirectionally you would be able to achieve 48Gbps in each direction for an aggregate of 96Gbps. You
are able to achieve a throughput of 48Gbps in total. For example, you could have 12Gbps of Southbound traffic (in and
out of the loadbalancer) and 36Gbps of Northbound traffic (in and out of the loadbalancer) for an aggregate 48Gbps total
throughput.
