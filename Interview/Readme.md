Here are the answers to all 55 AWS VPC-related interview questions, grouped into sections:

⸻

✅ Core AWS VPC Interview Questions (1–45)

🔹 VPC Basics & Components
	1.	What is a VPC in AWS? Why is it used?
A Virtual Private Cloud (VPC) is a logically isolated section of the AWS cloud where you can launch AWS resources in a virtual network that you define. It enables complete control over networking.
	2.	Main components of a VPC:
	•	Subnets
	•	Route Tables
	•	Internet Gateway (IGW)
	•	NAT Gateway
	•	Network ACLs (NACLs)
	•	Security Groups
	•	VPC Peering
	•	Elastic IPs
	•	Endpoints
	3.	Public vs Private Subnet:
	•	Public subnet has a route to an Internet Gateway.
	•	Private subnet doesn’t have a route to the IGW.
	4.	How does a private instance access the internet?
Via a NAT Gateway/Instance placed in a public subnet with route configured.
	5.	What is an Internet Gateway? Can you have more than one?
IGW is a horizontally scaled, redundant, and highly available VPC component that allows communication between instances in your VPC and the internet.
❌ Only one IGW per VPC.
	6.	What is a NAT Gateway? How is it different from NAT Instance?
NAT Gateway is a managed, scalable AWS service. NAT Instance is a self-managed EC2 instance.
	•	NAT Gateway is preferred for high availability and performance.
	7.	Limitations of NAT Instance vs NAT Gateway:
	•	NAT Instances require manual scaling and patching.
	•	NAT Gateway offers better throughput, redundancy, and automation.
	8.	Default VPC — use in production?
No. Always create a custom VPC in production for better isolation and control.
	9.	Subnets per VPC & spanning AZs?
	•	Max 200 subnets per VPC by default.
	•	A subnet resides in one AZ only.
	10.	Can CIDR block be modified after VPC creation?
Yes. You can add secondary CIDR blocks, but can’t change the primary.

⸻

🔹 Routing & Access
	11.	Connect two VPCs in different regions:
Use VPC Peering (cross-region) or Transit Gateway for complex multi-VPC communication.
	12.	Multiple route tables with a subnet?
❌ Only one route table can be associated per subnet.
	13.	Troubleshooting SSH to private EC2:

	•	Check route tables
	•	Bastion host setup
	•	SG/NACL rules
	•	Correct private key
	•	EC2 health/state

	14.	Restrict internet access to private subnet:

	•	Remove NAT Gateway route
	•	Set deny rules in NACLs

	15.	Delete IGW — what happens?
All instances in public subnets lose internet access.
	16.	Subnet accessing another VPC?

	•	Yes, via VPC Peering, Transit Gateway, or PrivateLink

	17.	VPC Peering vs Transit Gateway:

	•	Peering is 1:1, no transitive routing.
	•	TGW supports transitive routing, hub-and-spoke model.

	18.	Connect on-prem to AWS:

	•	Use Site-to-Site VPN, AWS Direct Connect, or Transit Gateway.

	19.	DNS in VPC:

	•	AmazonProvidedDNS resolves internal DNS.
	•	Enable/disable via DHCP options.

	20.	Asymmetric routing issue?
Check reverse path in route table, NAT Gateway/IGW routes, NACLs.

⸻

🔹 Security
	21.	Security Group vs Network ACL:

	•	SG = stateful, instance-level
	•	NACL = stateless, subnet-level

	22.	Which is stateful/stateless?

	•	SG = Stateful
	•	NACL = Stateless

	23.	Can SG be assigned to subnet?
❌ No. SGs are attached to ENIs (i.e., EC2 instances).
	24.	Restrict SSH to one private EC2:

	•	Use Bastion Host in public subnet
	•	SG allows only Bastion’s private IP

	25.	Restrict EC2 access to specific ports/IPs:

	•	Use SG rules (source IP, port range)

	26.	Deny rules in SGs?
❌ SGs only allow rules.
✅ Deny rules are possible in NACLs.
	27.	Inbound vs Outbound in SG/NACLs:

	•	SG: both needed (stateful)
	•	NACL: must explicitly allow both directions

⸻

🔹 Troubleshooting & Monitoring
	28.	Private instance can’t access internet:

	•	Check subnet routes
	•	NAT Gateway present and working
	•	SGs/NACLs allow outbound
	•	No overlapping CIDR

	29.	What is MTU in VPC?
Maximum Transmission Unit (usually 1500 bytes).
Check logs or use ping -s to test fragmentation.
	30.	VPC communication latency:

	•	Use VPC Flow Logs
	•	CloudWatch metrics
	•	Enhanced Networking (ENA)

⸻

🔹 Automation & Environment Design
	31.	Provision VPC via Terraform/CFN:
Use IaC to define VPC, subnets, route tables, gateways, etc.
	32.	Manage multiple environments:

	•	Use Terraform workspaces or different variable sets
	•	Isolate via separate VPCs or CIDR ranges

	33.	Terraform modules for VPC:

	•	terraform-aws-modules/vpc/aws
	•	Reusable, parameterized module

	34.	Isolate environments securely:

	•	Use different VPCs or subnets
	•	Apply proper SGs, NACLs, VPC endpoints

⸻

🔹 Design & Scalability
	35.	HA across AZs:

	•	Subnets in multiple AZs
	•	Multi-AZ NAT Gateways
	•	Load balancers spanning AZs

	36.	Subnetting best practices:

	•	Reserve separate CIDR blocks per AZ
	•	Avoid overlap
	•	Size subnets according to growth

	37.	Multiple CIDR blocks for VPC:

	•	Yes, to expand IP range
	•	Must not overlap

	38.	Why multiple route tables?

	•	Fine-grained control
	•	Different routes for public/private/data subnets

	39.	AWS PrivateLink vs Peering:

	•	PrivateLink = one-way, service-based access
	•	Peering = two-way traffic between VPCs

⸻

🔹 Logs & Observability
	40.	What is VPC Flow Logs?

	•	Logs all IP traffic in/out of network interfaces
	•	Used for troubleshooting, monitoring, compliance

	41.	Tools for monitoring VPC traffic:

	•	VPC Flow Logs
	•	CloudWatch
	•	3rd party NPM tools (e.g., Datadog, Wireshark)

	42.	Network segmentation in VPC:

	•	Subnets, route tables, NACLs
	•	Separate security groups

	43.	Elastic Network Interfaces (ENIs):

	•	Virtual NICs
	•	Allow multiple IPs, flexibility during scaling/failover

	44.	Default vs custom route tables:

	•	Default = attached to subnets by default
	•	Custom = used for specific routing needs

	45.	Secure VPC Endpoints:

	•	Use interface endpoints for private connectivity
	•	Restrict via security groups and policies

⸻

✅ VPC Peering & Site-to-Site VPN (46–55)
	46.	What is VPC Peering?
A networking connection between two VPCs to route traffic using private IPs.
	47.	Cross-account / cross-region VPC Peering?
✅ Supported

	•	Requires manual or automated setup in both VPCs
	•	Route tables must be updated

	48.	Transitive routing in VPC Peering?
❌ Not supported
Must use Transit Gateway for that.
	49.	CIDR overlap in peering?
❌ Peering will fail if CIDRs overlap.
	50.	Limitations of VPC Peering:

	•	No transitive routing
	•	Limited to 125 peering connections per VPC (default)
	•	Must update routes manually

	51.	Route table configuration in VPC Peering:
Each side must add routes to the other VPC’s CIDR via the peering connection.
	52.	Secure VPC Peering traffic:
Use SGs and NACLs
Private IP traffic only
	53.	Billing in VPC Peering:

	•	Data transfer between AZs is charged
	•	No charge for data in same AZ

	54.	Multiple VPCs with Peering?
Possible but complex.
Prefer Transit Gateway for >2 VPCs.
	55.	Site-to-Site VPN troubleshooting:

	•	Check tunnel status
	•	BGP status
	•	CloudWatch metrics
	•	On-prem firewall rules
	•	VPN logs in CloudWatch
