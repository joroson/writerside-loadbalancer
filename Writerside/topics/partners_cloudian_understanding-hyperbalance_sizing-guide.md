<show-structure for="chapter,procedure" depth="2"/>
# Sizing Guide

## HyperBalance Models

| Model                | HBL-VM | HBL-1050 | HBL-1100 |
|----------------------|--------|----------|----------|
| Sustained Throughput | 8 Gbps | 40 Gbps  | 70 Gbps  |

## Hardware Specifications

You should always use Cloudian HyperBalance hardware or validated hardware. In some cases, this is not possible due to
import/export legislation, corporate governance, etc. When this is not possible and an installation needs to be
delivered on third-party hardware, it must exceed these specifications.

## Minimum specifications

| Item    | HBL-1050         | HBL-1100         | Notes                                                                                                                                                |
|---------|------------------|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| CPU     | 6C12T @ 2.5GHz   | 24C48T @ 2.5GHz  | Intel CPUs                                                                                                                                           |
| RAM     | 16GB @ 3200 MT/s | 32GB @ 3200 MT/s | Where possible, all memory channels should be populated                                                                                              |
| Storage | >250GB           | >250GB           | OS requirement is 20GB. No RAID, neither hardware or software is supported. NVMe/SSD/HDD supported.                                                  |
| Network | 2 x 25GbE        | 1 x 100GbE       | Supported adapters: Supported adapters: Mellanox: MCX512A-ACAT, MCX516A-GCAT, MCX516A CCAT, MCX516A-CDAT. Other vendors are not currently supported. |
| PCIe    | Gen 3.0 x16      | Gen 4.0 x16      | Minimum requirements to satisfy bus speed.                                                                                                           |


## Considerations

### Throughput

The amount of data, usually referred to as traffic, being (or capable of being) transmitted and received ‘over the
network’ by a device such as a load balancer or server, per second. You may also be able to monitor the throughput of a
VIP but this will always be limited by the capabilities of the device it exists on. Typically the maximum throughput of
a load balancer is determined by the maximum throughput (or speed) of all of its network interfaces combined. As
interface speeds get higher this rule of thumb becomes harder to achieve. Keep in mind also that protocol overheads mean
that it is almost impossible ever to achieve full wire speed for a particular interface. Throughput is generally 80% of
the listed maximum interface speed for a given Network Interface Card.
The achievable throughput for a device can also depend on myriad other factors, including what the appliance is having
to process. For example, additional packet manipulation, custom health checking, or additional processes.

### Concurrent Users

To get an understanding of the estimated load the platform will be required to support, you should first know how many
users it is expected to be used by. Not only how many users will be accessing the platform but also when they will be
accessing it. Are the users geographically dispersed across time zones? Will everyone be using it at the same time? Or,
will there be peaks and troughs throughout the day? When you have an understanding or an expectation of how users will
interact with the platform you will be able to build a picture of what kind of throughput those users will generate.
Of course, not all users are people and a HyperStore cluster can be used by programs and applications. In fact, they
will probably make up the majority of the load that goes through the platform. You will also need to account for events
like automated backups and the load that they will generate.

### Peak times

How much data is moving through the network at peak times? Relying on the average network load/throughput as your
benchmark will inevitably lead to problems. Sizing a solution based on peak network utilisation instead of average
network utilisation is the best method. For example, restoring application servers after a failure or outage through an
HBL-1100 will take around half the time it will through an HBL-1050. Not installing a right-sized HyperBalance system
could mean missing the Recovery Time Objective.

### Future expansion
This is an often-cited statistic, but it bears repeating

> “90% percent of the world’s data was created in the last two years. And every two years, the volume of data across the
world doubles in size.”{style="note"}

It is something worth keeping in mind whilst sizing not only your HyperStore Cluster but also your HyperBalance needs.

Always factor in the likelihood that the number of users of a HyperStore cluster will scale greatly. Over and above
that, you need to consider the likelihood that your HyperStore Cluster itself will scale greatly. Both these scenarios
are very often the case once the business realises just how vital a HyperStore Cluster becomes for day-to-day
operations.

HyperBalance is able to operate at sustained throughputs of 40 Gbps (HBL-1050) and 70 Gbps (HBL-1100). That means an
HBL-1050 can read or write 18 TB/hr and 432 TB/day. The HBL-1100 can read or write 31.5 TB/hr which is 756 TB/day to a
HyperStore Cluster.

There are not any HyperStore Clusters currently deployed that are bandwidth constrained by an in-path load balancing
solution. However, whilst that is currently the case, that will not necessarily always be the case. In a deployment
where the sustained throughput is above the capability of the HyperBalance, the system can be deployed configured with
Smart DNS.