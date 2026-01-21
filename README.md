Secure-AWS-VPC-Project-.Secure AWS VPC Infrastructure Deployment

This project focuses on the design and implementation of a secure Amazon Web Services (AWS) Virtual Private Cloud (VPC) using a tiered network architecture. The infrastructure is designed to ensure that resources hosted in a private subnet are able to access the internet securely for outbound traffic (such as software updates) while remaining inaccessible from direct inbound connections originating from the public internet.

The project follows AWS networking best practices by separating public-facing and private resources, implementing controlled routing, and enforcing security boundaries using gateways, route tables, and network access control lists.

Project Objectives

The objectives of the project are as follows:

Design and deploy an AWS VPC using the CIDR block 10.0.0.0/16
Create a public subnet and a private subnet within the same Availability Zone
Enable internet access for public resources using an Internet Gateway
Enable secure outbound internet access for private resources using a NAT Gateway
Prevent direct inbound access to resources hosted in the private subnet
Apply routing and security controls to support a secure tiered architecture
Provide documentation and visual proof of the deployed infrastructure

Architecture Overview

The architecture consists of a single VPC containing two subnets:

A Public Subnet that allows direct access to the internet
A Private Subnet that does not allow direct inbound internet access

The public subnet hosts a NAT Gateway, which enables resources in the private subnet to initiate outbound internet connections while maintaining security isolation.

![Secure AWS VPC Architecture Diagram]https://github.com/Thelezinhle/Secure-AWS-VPC-Project-./blob/main/architecture-diagram.drawio.png

Network Configuration Details

VPC Configuration

VPC CIDR Block: 10.0.0.0/16
VPC ID: vpc-035686006b832dbfb
Cloud Provider: Amazon Web Services (AWS)
Region: us-east-1 (N. Virginia)
Availability Zone: us-east-1a

Subnet Configuration

| Subnet Type    | CIDR Block   | Description                                              |
| -------------- | ------------ | -------------------------------------------------------- |
| Public Subnet  | 10.0.10.0/24 | Hosts public-facing resources and the NAT Gateway        |
| Private Subnet | 10.0.1.0/24  | Hosts protected resources with no direct internet access |

Both subnets are deployed within the same Availability Zone to meet project requirements.

Connectivity and Routing

Internet Gateway

An Internet Gateway is attached to the VPC to enable internet connectivity. The public subnet is associated with a route table that directs outbound internet traffic to the Internet Gateway.

Internet Gateway ID: igw-0005c508ed50aa709
Status: Attached to VPC

NAT Gateway

A NAT Gateway is deployed within the public subnet. This gateway allows resources in the private subnet to access the internet for outbound connections while blocking unsolicited inbound traffic from the public internet.

NAT Gateway ID: nat-061d21077f33ac006
Public IP: 52.21.153.230
Private IP: 10.0.10.15
Status: Available

Route Tables

Separate route tables are configured for each subnet:

Public Subnet Route Table
Route Table ID: rtb-0f7dd4710251b2856
Route: 0.0.0.0/0 → Internet Gateway (igw-0005c508ed50aa709)
Associated Subnet: Public-Subnet (10.0.10.0/24)

Private Subnet Route Table
Route Table ID: rtb-0f94e3db4cb8b5705
Route: 0.0.0.0/0 → NAT Gateway (nat-061d21077f33ac006)
Associated Subnet: Private-Subnet (10.0.1.0/24)

This routing configuration ensures secure traffic flow and enforces subnet isolation.

Security Controls

Security Groups
Bastion Security Group: Allows SSH access (port 22) from trusted IP addresses only
Private Instance Security Group: Allows SSH access only from the Bastion Security Group

Network Access Control Lists (NACLs)

Network Access Control Lists (NACLs) are applied at the subnet level to control inbound and outbound traffic. The NACL configuration supports the separation between public and private subnets and contributes to the overall security posture of the network.

Connectivity Testing and Validation

To validate the network configuration, we ensured that resources in both subnets behave as intended:

**Private Subnet:** Outbound internet access is enabled through the NAT Gateway located in the public subnet. A test EC2 instance deployed in the private subnet has no public IP and no inbound security group rules, ensuring it cannot be accessed directly from the internet. This setup confirms that private resources can initiate outbound connections while remaining protected from direct inbound access.

Public Subnet: Resources in the public subnet have direct internet access via the Internet Gateway, as configured in the public route table.

These validations confirm that the security and connectivity requirements of the project have been met.

To validate the network configuration, the following tests are performed:

A resource deployed in the private subnet is able to initiate outbound internet connections (e.g., software updates), confirming correct NAT Gateway configuration.
Attempts to directly access the private subnet from the public internet fail, confirming that private resources are not publicly reachable.

These tests demonstrate that the security and connectivity requirements of the project have been met.

Evidence and Screenshots

The following screenshots are included in the `/screenshots` directory as proof of the deployed infrastructure:

VPC Configuration: Showing CIDR block 10.0.0.0/16
Subnet Details: Public and private subnet configurations
Route Table Associations: Public and private route table configurations
NAT Gateway Status: NAT Gateway with public IP assignment
Internet Gateway Attachment: IGW attached to the VPC
EC2 Instances: Bastion Host and Private Instance configurations

![VPC CIDR Block]
![Public Subnet Details]
![Private Subnet Details]
![Internet Gateway Attachment]
![NAT Gateway Status]
![Public Subnet Route Table]
![Private Subnet Route Table]
![Bastion Host Details]
![Private Instance Details]

Conclusion

This project successfully demonstrates the implementation of a secure AWS VPC architecture using industry best practices. By separating public and private resources, controlling routing paths, and enforcing security boundaries, the infrastructure ensures both functionality and protection of sensitive resources within the cloud environment.

The deployment achieves:

1. Security: Private resources are inaccessible from the public internet
2. Functionality: Private resources can access the internet via NAT Gateway for updates
3. Compliance: Follows AWS best practices for network segmentation
4. Scalability: Architecture can be extended with additional subnets and services

Future Improvements

Future improvements to this project could include:

Implementing VPC Flow Logs for network traffic monitoring
Adding a Web Application Firewall (WAF) for enhanced security
Implementing Auto Scaling Groups for high availability
Adding a Load Balancer for distributing traffic
Implementing AWS VPN or Direct Connect for hybrid cloud connectivity
Adding multiple Availability Zones for disaster recovery
Implementing AWS Transit Gateway for multi-VPC connectivity

Contact Information

For any questions or concerns, please contact Thelezinhe Buthelezi on [GitHub](https://github.com/Thelezinhle)

License

This project is for educational and demonstration purposes. Feel free to use it as a reference for your own AWS VPC implementations.

---

Last Updated: January 2026  
AWS Region: us-east-1  
Project Status: ✅ Successfully Deployed and Tested
