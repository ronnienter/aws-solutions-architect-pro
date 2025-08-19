
## 1. Introduction to AWS Networking Concepts
------------- ~~~~~~
Scenario
A global fintech startup needs to process millions of transactions daily with bank-level security, multi-region support, and seamless operations. Running entirely in the public cloud without control is like operating a bank in an open square.

Amazon VPC

Amazon Virtual Private Cloud (VPC) provides a private, secure slice of the AWS cloud where you fully control your network environment.

- Comparable to a physical bank: controlled access points, private vaults, secure communication channels.

- Enables isolated network environments, precise traffic flow control, security boundaries, and connectivity options.


Key Learning Goals:

- Design secure and high-performance network topologies.

- Implement hybrid cloud connectivity patterns.

- Leverage advanced networking features to reduce bottlenecks and optimize costs.








## 2.  Amazon VPC and Core Components


// Amazon VPC

Amazon VPC (Virtual Private Cloud): Logically isolated section of AWS Cloud where you define virtual networking.

- You control CIDR ranges, subnets, route tables, gateways, security.

- Ensures network isolation, compliance, and security.

- Each account includes a default VPC per Region, but custom VPCs are recommended for production.



// Core Components
1. IP Address Space Management

- VPC uses a CIDR block (from RFC 1918).

- Cannot be changed after creation.

- Plan for scaling and avoid overlaps with on-prem networks.


2. Subnets (Network Segmentation)

- Subnets divide VPC IP space; single Availability Zone only.

- Foundation for isolating workloads and tiers. 

Types:

Public Subnet → routes via Internet Gateway; hosts web servers, NAT gateways.

Private Subnet → no inbound internet; hosts databases, internal apps.


Planning:

AWS reserves 5 IPs per subnet.

Use larger subnets + granular controls vs. many small subnets for better scalability.



3. Route Tables

Define traffic direction for subnets.

All VPCs include a default local route (cannot be removed).


Custom Routes:

Support IGW, VPC Peering, VPN, Direct Connect.

Separate route tables for public vs private subnets.



Rules:

Longest prefix match decides routing.

Static routes > (over) propagated routes.

Propagation (VPN/Direct Connect) simplifies setup but must avoid conflicts.




4. Internet Gateway (IGW): VPC Internet Connectivity

Region-level, attaches to one VPC.

Enables internet connectivity for public subnets.

Provides scalable NAT for public IP traffic.



Public IP Options:

Auto-assigned (ephemeral).

Elastic IPs (static, account-owned). Useful for fault tolerance and consistent endpoints.



Security:

IGW does not expose resources unless:

Instance has a public IP.

Route table points to IGW.

Security Groups + NACLs add protection layers.


