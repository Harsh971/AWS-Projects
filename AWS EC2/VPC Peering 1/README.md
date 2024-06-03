# AWS VPC Peering Project

## Project Overview
         
<img src="https://github.com/Harsh971/AWS-Projects/blob/main/AWS%20EC2/VPC%20Peering%201/architecture.png"></img>

This project involves the creation of two distinct Virtual Private Clouds (VPCs), each containing public subnets and a single EC2 instance. The objective is to establish communication between the instances in different VPCs using VPC Peering-like architecture through Internet Control Message Protocol (ICMP), specifically using ping commands.

## Architecture Design

### VPC Configuration

#### VPC 1
- **VPC CIDR**: 10.0.0.0/16
- **Public Subnet**: 10.0.1.0/24
- **Availability Zone**: us-east-1a
- **EC2 Instance**: Instance 1 (IP: 10.0.1.10)

#### VPC 2
- **VPC CIDR**: 10.1.0.0/16
- **Public Subnet**: 10.1.1.0/24
- **Availability Zone**: us-east-1b
- **EC2 Instance**: Instance 2 (IP: 10.1.1.10)

### Networking Components

#### Route Tables
- **Route Table for VPC 1**: Configured to route traffic to VPC 2's subnet
  - Destination: 10.1.0.0/16
  - Target: VPC Peering Connection (pcx-xxxxxx)
  
- **Route Table for VPC 2**: Configured to route traffic to VPC 1's subnet
  - Destination: 10.0.0.0/16
  - Target: VPC Peering Connection (pcx-xxxxxx)

#### Security Groups
- **Security Group for Instance 1 (VPC 1)**:
  - Inbound Rule: Allow ICMP (Ping) from VPC 2's CIDR (10.1.0.0/16)
  
- **Security Group for Instance 2 (VPC 2)**:
  - Inbound Rule: Allow ICMP (Ping) from VPC 1's CIDR (10.0.0.0/16)

### VPC Peering Connection
- A VPC Peering Connection is established between VPC 1 and VPC 2 to allow routing of traffic between them.

## Steps for Implementation

1. **Create VPCs and Subnets**:
   - Create VPC 1 with CIDR block 10.0.0.0/16.
   - Create a public subnet within VPC 1 (10.0.1.0/24) in us-east-1a.
   - Launch an EC2 instance within the public subnet of VPC 1.
   
   - Create VPC 2 with CIDR block 10.1.0.0/16.
   - Create a public subnet within VPC 2 (10.1.1.0/24) in us-east-1b.
   - Launch an EC2 instance within the public subnet of VPC 2.

2. **Configure Route Tables**:
   - Modify the route table of VPC 1 to route traffic to 10.1.0.0/16 via VPC Peering Connection.
   - Modify the route table of VPC 2 to route traffic to 10.0.0.0/16 via VPC Peering Connection.

3. **Set Up Security Groups**:
   - For the instance in VPC 1, create a security group that allows inbound ICMP traffic from 10.1.0.0/16.
   - For the instance in VPC 2, create a security group that allows inbound ICMP traffic from 10.0.0.0/16.

4. **Establish VPC Peering Connection**:
   - Create a VPC Peering Connection between VPC 1 and VPC 2.
   - Accept the VPC Peering Connection request in both VPCs.
   - Update route tables in both VPCs to include routes for the other VPC.

5. **Verification**:
   - SSH into the instance in VPC 1.
   - Ping the instance in VPC 2 using its private IP address to verify connectivity.
   - SSH into the instance in VPC 2.
   - Ping the instance in VPC 1 using its private IP address to verify connectivity.

