# Public vs Private subnets

Take from the [AWS VPC docs](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Subnets.html#vpc-subnet-basics)

*If a subnet's traffic is routed to an internet gateway, the subnet is known as a public subnet*. 
If you want your instance in a public subnet to communicate with the 
internet over IPv4, it must have a public IPv4 address or an Elastic IP address (IPv4).

*If a subnet doesn't have a route to the internet gateway, the subnet is known as a private subnet.*

If a subnet doesn't have a route to the internet gateway, but has its traffic routed to a virtual private 
gateway for a VPN connection, the subnet is known as a VPN-only subnet. 


# Subnet Routing

Each subnet must be associated with a route table, which specifies the allowed routes for outbound traffic 
leaving the subnet. Every subnet that you create is automatically associated with the main route table for 
the VPC. You can change the association, and you can change the contents of the main route table.

In the previous diagram, the route table associated with subnet 1 routes all IPv4 traffic (0.0.0.0/0) and 
IPv6 traffic (::/0) to an internet gateway (for example, igw-1a2b3c4d). Because instance 1A has an 
IPv4 Elastic IP address and instance 1B has an IPv6 address, they can be reached from the internet 
over IPv4 and IPv6 respectively.

The instance 2A can't reach the internet, but can reach other instances in the VPC. You can allow an 
instance in your VPC to initiate outbound connections to the internet over IPv4 but prevent unsolicited 
inbound connections from the internet using a network address translation (NAT) gateway or instance. 
Because you can allocate a limited number of Elastic IP addresses, we recommend that you use a NAT device 
if you have more instances that require a static public IP address. For more information, see NAT. To 
initiate outbound-only communication to the internet over IPv6, you can use an egress-only internet gateway. 
For more information, see Egress-Only Internet Gateways.
