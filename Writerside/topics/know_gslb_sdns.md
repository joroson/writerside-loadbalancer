# Smart DNS

<show-structure for="chapter,procedure" depth="2"/>

## What is SDNS?

It used to be known as GSLB direct-to-node. SDNS (Smart DNS) is a way of implementing Global Server Load Balancing in a
specific way to leverage the benefits of round-robin DNS whilst dropping some of the biggest problems with it. We have
extended the functionality to also tie in to customer environments and serve DNS responses intelligently based on server
utilisation/availability. SDNS seems to be largely misunderstood as it appears to be considered a panacea of sorts. It
is an extremely useful tool to have available to you but it is not a cure-all.

## When is SDNS the answer?

When we consider the use case of a Cloudian HyperStore cluster SDNS is useful at the extremes of the deployment
methodology. It is useful in extremely small clusters that don’t need actual load balancing and then is useful again in
large clusters. The small cluster breakpoint is dependent on many factors. When plans are set in place to scale out the
cluster there should also be an evaluation of whether or not the HyperBalance appliances need to be upgraded too. On the
upper end of the scale, SDNS becomes a necessity when the HyperBalance appliances are unable to keep up with the amount
of data that is going through them (70 Gbps sustained). As good as SDNS is, it should really only be used when the
environment satisfies these requirements and is therefore most beneficial to the workload. An example of when SDNS is an
appropriate solution: You have a Loadbalancer appliance that has 10GbE connectivity, the rest of your servers have been
upgraded to 25GbE NICs, your top-of-rack switches are connected into the distribution layer at 100GbE, and your Data
Center Interconnects are bundled 100GbE connections. This is the kind of scenario where your Load Balancers could be the
bottleneck. In this instance you could implement SDNS as an interim solution to alleviate the bottleneck whilst the load
balancer connection is upgraded.

## When is SDNS not the answer?

The majority of installations should work better with a ‘traditional’ HyperBalance deployment, meaning that SDNS is not
implemented. As previously stated, SDNS is best used on extremely small and extremely large clusters. If your
environment is not suffering consistently high system utilisation then you probably don’t need to implement SDNS.

## The big question

The question that we use to determine whether or not SDNS is a requirement is

> “What speed is the connection between the load balancers and the clients?”

This is a crucial consideration as it doesn’t matter what you put in place between everything else if your clients are
limited by their connection to the load balancers. Requests to your infrastructure can only ever be as fast as the
slowest link in the path to your chosen destination.

If your load balancer is not suffering from extremely high load, be it CPU or network utilisation for the majority of
the time, you don’t need to implement SDNS.
What are the benefits?

- It works and is Reliable, Fast, Tunable, unlimited scalability and low-resource utilisation (i.e. cheaper).
- Works better and better with more servers/clients and more traffic, unlike layer 7, which has fixed limitations and
  higher resource requirements.
- It is only limited by the speed of the network infrastructure.
- Dynamic weighting, it is able to adjust the distribution of requests based on environmental factors
- TTL0 for bursty workloads. You can implement a Time To Live of 0 for the responses sent by SDNS, this provides
  requesters with the most up-to-date information and allows for better distribution of requests amongst the configured
  real servers.
- It's a hell of a lot better than using alternatives like Active directory round robin!

## What are the pitfalls?

- Reliant on local DNS infrastructure which may need optimisation.
- Clients might need to be configured too, DNS caching is enabled on most clients to reduce unnecessary DNS traffic. DNS
  is nowhere near as dynamic as SDNS requires it to be as records are typically static.
- Pretty much all the benefits of load balancing are lost. Most importantly, session persistence, connection tracking,
  and content switching are completely lost to you.
- It doesn’t fail gracefully, if SDNS fails you just won’t receive a response to the query/request that you sent.

## SDNS Testing

### What do we test?

At the time of writing the testing is still being developed. However, the test involves bombarding the SDNS server with
as many DNS lookups as possible in as short an amount of time as possible.

### How do we test?

The current test set up is a script that generates a given amount of requests to a SDNS enabled load balancer. At the
moment it takes in the following configuration variables:

- (S)DNS Server.
- FQDN (what to resolve).
- Record Type (A, AAAA, etc.).
- Number of requests.
- Concurrency/parallelisation/threads.

With those variables in place, the script generates as many DNS requests as possible to the configured server and
records each response. Once complete, the results are saved as a JSON file providing the following information:

- **dns_server:** The DNS server that the test was run against.
- **threads:** The concurrency setting that was used.
- **num_requests:** The amount of requests that were sent.
- **test_duraton_msecs:** The amount of time that the test took to complete.
- **average_response_msecs:** The average response time computed from all responses.
- **responses:** A list of all the DNS responses received providing the following information:
- **fqdn:** Queried FQDN.
- **record_type:** Record Type returned.
- **resolution_time:** The amount of time the resolution took in milliseconds.
- **responses:** Record response(s) in a JSON list.
- **epoch_timestamp_millis:** Timestamp required for graphing, etc.

This generates a JSON file containing all of the responses and times along with the computed averages. Depending on the
number of requests configured for the particular test, these can generate quite large JSON files. For example, a 10,000
request test generates a 2.7MB file. A 50,000 request test generates a 13.5MB file.

### What are the numbers?

The initial findings from the testing that has happened is that the limiting factor is the device that the test is being
run from. A distributed test in a dedicated environment is required to get a firm understanding of what the upper limit
is, this is in planning. The firm numbers that we currently have are 6600 RPS (responses per second) from a single (
high-powered) host and 5000 RPS from a test distributed amongst four client VMs in a virtualisation environment
suffering from high contention. These results bear out the statement that the test device is the limiting factor at this
point in time.

#### 10,000 Request Test

![10000 Request Test](10000_Requests_SDNS.png)

#### 50,000 Request test

![50000 Request Test](50000_Requests_SDNS.png)

#### SDNS Response times @ 5000 RPS

![5000 Requests Per Second Response Time Graph](5000_RPS_Response_Graph.png)

The above graph illustrates the response times for a 50,000 request test over time (approximately 11 seconds). The
initial burst of responses are slower and then the results are returned much faster once the process ramps up.

#### SDNS System utilisation @ 5000 RPS

![5000 Requests Per Second System Utilisation](5000_RPS_System_Usage.png)

The above graph displays the system utilisation for the SDNS server over the period of the test. This particular SDNS
server is a VM configured with 4vCPU and 8GB vRAM. The only resource that is affected by the test is CPU and that hits a
maximum of 54% utilisation over the period of the test.

#### What do the numbers mean?

At this stage we are hesitant to do much in the way of extrapolating the data to produce as the results are unlikely to
scale linearly. However, the results that we have at the moment allow us to expand the data as follows:

<table>
  <tr><th colspan="2">SDNS operating @5000 RPS</th></tr>
  <tr><th>Request Size</th><th>Aggregate Throughput</th></tr>
  <tr><td>1 kB</td><td>0.04 Gbps</td></tr>
  <tr><td>128 kB</td><td>5.12 Gbps</td></tr>
  <tr><td>256 kB</td><td>10.24 Gbps</td></tr>
  <tr><td>512 kB</td><td>20.48 Gbps</td></tr>
  <tr><td>1 MB</td><td>40.96 Gbps</td></tr>
  <tr><td>512 MB</td><td>20.48 Tbps</td></tr>
  <tr><td>1 GB</td><td>40 Tbps</td></tr>
</table>

## Considerations

SDNS does not fail anywhere near as gracefully as Layer 7, responses are simply not returned to the requester. By
comparison, Layer 7 fails very gracefully. For example, if you have a 10G load balancer and ask it for 20G of traffic
all the
requests will succeed, they will just have more latency.

## Errata

SDNS used to be referred to as GSLB Direct-to-node. The names are synonymous, but going forward we are using SDNS as it
is less of a mouthful.
