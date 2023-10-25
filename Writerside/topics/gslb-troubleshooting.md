# Troubleshooting

## EDNS-CS

Support for **E**xtension mechanisms for **D**omain **N**ame **S**erver - **C**lient **S**ubnet (EDNS-CS) was introduced
to the Enterprise appliances from version 8.11. The principal method of troubleshooting issues with client subnet
evaluation is to first log the entries that are being observed by PDNS to ensure that EDNS-CS information is correctly
being sent to the GSLB for evaluation against the topology file.


<procedure title="Enabling PDNS logging" id="enable-pdns-logging">
    <step>Open the <code>/etc/pdns/pdns.conf</code> file in your preferred editor.</step>
    <step>
        <p>Add the following lines to the end of the <code>pdns.conf</code> file and save it.</p>
        <code-block lang="shell">
            loglevel=7
            log-dns-queries=yes
            log-dns-details=yes
        </code-block>
    </step>
    <step>
        <p>Restart the PDNS service</p>
        <code-block lang="shell" prompt="[root@lbprimary ~]#">
            service pdns restart
        </code-block>
    </step>
</procedure>

Once PDNS logging is set to the appropriate level and the service has been restarted, the dns queries are being logged
to `/var/log/messages`. So, you can tail that file to see the DNS queries that are coming in. When we are talking about
troubleshooting issues with Extended DNS Client Subnet (EDNS-CS)

```Shell
Feb 30 12:34:56 lbprimary pdns[9001]: Remote 10.100.0.10<-192.168.65.0/24 wants 'cloudy.with.meatballs|A', do = 0, bufsize = 1232 (4096)
Feb 30 12:34:56 lbprimary pdns[9001]: Remote 10.100.0.10 wants 'cloudy.with.meatballs|A', do = 0, bufsize = 1232 (4096)
```

In this case, the information that we are most concerned with is the Remote IP, the GSLB uses this to match against the
topologies configured in the load balancer. If there is an issue with the Remote IP that is being offered up to the GSLB
that can cause issues with "TWRR" working the way that we need it to.

The first request is showing us the following

```Shell
Remote 10.100.0.10<-192.168.65.0/24 wants 'cloudy.with.meatballs'
```

What this is telling us is that the actual request that came in to the GSLB is sourced from 10.0.51.14 but the Client
Subnet field has been set with the originating client subnet configured as 192.168.65.0/24. As the client subnet field
is set, that is what the GSLB will use to evaluate against the topology configuration. The client subnet field can be
set if the DNS request originates from a completely different than the IP address that has forwarded the address to the
GSLB, in this case it is because I manually set the field on the lookup, like so

```Shell
dig @192.168.100.80 cloudy.with.meatballs +subnet=192.168.65.0/24
```

The second request doesn't have the extra information of the Client Subnet field

```Shell
Remote 10.100.0.10 wants 'cloudy.with.meatballs'
```

With this lookup the remote IP will be evaluated against the remote IP as the Client Subnet field is not set. This
request came in after issuing this command on the client

```Shell
nslookup cloudy.with.meatballs 192.168.100.80
```

The dns server was manually set as my dns server is not set up to point at the GSLB for this domain so a manual override
was used.

With the information from the PDNS logging you will be able to ascertain whether the DNS requests are coming from the
correct location. You will also be able to see if the Client Subnet field has been populated. With these points of
information in hand you should be able to understand whether the issue is in the topology configuration, the DNS
infrastructure, or some other part of the platform. 