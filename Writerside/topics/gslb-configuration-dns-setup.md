# DNS Setup

Before the Global Server Load Balancing and it's configuration can be tested in a meaningful way, the corresponding
network configuration will need to be in place.

## DNS Infrastructure

Generally speaking, you will want to sort out the DNS delegation and configuration for the network before you go to
configure the GSLB on the load balancer appliances. Unfortunately, this can be one of the most confusing parts of a GSLB
implementation too so getting it right in the first place is not exactly straightforward. For the products that have
deployment guides, it is worth reading those first as some of them contain product specific DNS delegation guidance.

## Windows Servers

## Other

There are so many different ways that DNS is implemented that it is simply not feasible to provide information on all of
the myriad ways. If you are running something other than a Windows-based DNS infrastructure then we can (rightly or
wrongly) assume that you know what you are doing.

The simple answer to how the designated subdomains are delegated is via NS DNS records. You CAN also do this via
conditional forwarding. The end result that you want is for requests to the configured global names to be resolved by
the GSLBs running on the load balancer appliances.