# Public vs Private subnets

[AWS docs](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Subnets.html#vpc-subnet-basics)

*If a subnet's traffic is routed to an internet gateway, the subnet is known as a public subnet*. 
If you want your instance in a public subnet to communicate with the 
internet over IPv4, it must have a public IPv4 address or an Elastic IP address (IPv4).

*If a subnet doesn't have a route to the internet gateway, the subnet is known as a private subnet.*

If a subnet doesn't have a route to the internet gateway, but has its traffic routed to a virtual private 
gateway for a VPN connection, the subnet is known as a VPN-only subnet. 
