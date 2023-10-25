# The Loadbalancer.org Appliances

Understanding why we refer to our products as appliances is a good place to start. By definition it is a device or piece
of equipment designed to perform a specific task. It is applicable to our appliances because they are designed to
perform the specific tasks of load balancing and nothing else. That is, you are not able to install additional software
components on them.
There are three principle methods of delivering/installing Loadbalancer.org appliances in a customer environment.

- Hardware Appliance
- Virtual Appliance
- Cloud Appliance

The best deployment method for a customer can depend on many factors and is not something that can easily be distilled
into a few neat paragraphs.

## Hardware

Hardware deployments are either on the customer premises or in the customer data centre. Data centres are, for the most
part, at colocation facilities. The hardware appliances are provided by Loadbalancer.org and are built and sent from our
warehouse to order. The latest specifications for the hardware appliances can
be [found here](https://www.loadbalancer.org/products/hardware/).

<table>
    <tr>
        <td colspan="2">Where hardware is an appropriate platform</td>
    </tr>
    <tr>
        <th>Preferred</th>
        <th>Not preferred</th>
    </tr>
    <tr>
        <td>Throughput requirement exceeds the ability of a virtualised platform</td>
        <td>Customer doesn’t support hardware appliances. For example, HPE Green Lake or AWS Outpost environments.</td>
    </tr>
    <tr>
        <td colspan="2">The benefits and limitations of a hardware platform</td>
    </tr>
    <tr>
        <td>Benefits</td>
        <td>Limitations</td>
    </tr>
    <tr>
        <td>There is no contention of resources. The appliance is correctly sized for it’s use case and has access to all of the required compute at all times.</td>
        <td>Migrations (vMotion, etc.) is not a possibility.</td>
    </tr>
    <tr>
        <td>Network throughput is higher with hardware appliances as 100GbE NICs are available.</td>
        <td>Hardware upgrades are not as simple as they are in virtualised environments.</td>
    </tr>
</table>

## Virtual

Virtual installations are those that exist on a Type 2 Hypervisor can be located almost anywhere.

<table>
    <tr>
        <td colspan="2">Where virtualisation is an appropriate platform</td>
    </tr>
    <tr>
        <th>Preferred</th>
        <th>Not preferred</th>
    </tr>
    <tr>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td colspan="2">The benefits and limitations of a virtual platform</td>
    </tr>
    <tr>
        <th>Benefits</th>
        <th>Limitations</th>
    </tr>
    <tr>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td></td>
        <td></td>
    </tr>
</table>

## Cloud

Cloud installations are those that are destined to be installed on one of the major cloud providers that are supported
by default. Those cloud providers are:

- Amazon Web Services (AWS).
- Azure.
- Google Cloud Platform (GCP).

<table>
    <tr>
        <td colspan="2">Where cloud is an appropriate platform</td>
    </tr>
    <tr>
        <th>Preferred</th>
        <th>Not preferred</th>
    </tr>
    <tr>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td colspan="2">The benefits and limitations of a cloud platform</td>
    </tr>
    <tr>
        <th>Benefits</th>
        <th>Limitations</th>
    </tr>
    <tr>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td></td>
        <td></td>
    </tr>
</table>