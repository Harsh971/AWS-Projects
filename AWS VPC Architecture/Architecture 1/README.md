# VPC Architecture with 2 Availability Zones

This project illustrates the setup of a Virtual Private Cloud (VPC) architecture with two Availability Zones (AZs). The architecture includes a public subnet in AZ1 and a private subnet in AZ2. Each subnet contains one EC2 instance.

<img src="https://github.com/Harsh971/AWS-Projects/blob/main/AWS%20VPC%20Architecture/Architecture%201/architecture.png"></img>

## Components

- **VPC**: Virtual Private Cloud, providing isolated network space.
- **Subnets**:
  - **Public Subnet (AZ1)**: Connected to the internet through an Internet Gateway.
  - **Private Subnet (AZ2)**: Not directly accessible from the internet.
- **EC2 Instances**: Virtual servers running within the VPC.
- **Internet Gateway (IGW)**: Allows communication between instances in the VPC and the internet.
- **NAT Gateway**: Provides internet access to instances in the private subnet.

## Configuration Details

### 1. VPC Setup

- Create a VPC with CIDR block range.
- Create two subnets in different AZs: one public and one private.

### 2. Public Subnet (AZ1)

- Attach an Internet Gateway to the VPC.
- Associate the public subnet with the Internet Gateway.
- Launch an EC2 instance in the public subnet.

### 3. Private Subnet (AZ2)

- Create a NAT Gateway in the public subnet.
- Modify the route table of the private subnet to route internet traffic through the NAT Gateway.
- Launch an EC2 instance in the private subnet.

## Benefits

- **Security**: Isolate resources in private subnets from direct internet access.
- **High Availability**: Utilize multiple availability zones for redundancy and fault tolerance.
- **Scalability**: Easily scale resources horizontally by adding more instances or vertically by upgrading instance types.
- **Cost-Effectiveness**: Optimize costs by leveraging a combination of public and private resources.

## Reference

- TrainWithShubham : <a href="https://www.youtube.com/watch?v=UVNVPquIkXE&list=PLlfy9GnSVerTB0twnC5eaGD-oiHprpnW-">Click Here</a>
- Abhishek Veeramalla : <a href="https://www.youtube.com/watch?v=P8g7Z4NYk3Q&pp=ygUbYXdzIHZwYyBhYmhpc2hlayB2ZWVyYW1hbGxh">Click Here</a>

## Feedback

Your feedback is valuable! If you have suggestions for improving existing content or ideas for new additions, please open an issue or reach out to the repository maintainers. If you have any other feedbacks, you can reach out to us at harsh.thakkar0369@gmail.com


## Connect with Me
<p>

 <a href="https://twitter.com/HarshThakkar971" target="blank"><img align="center" src="https://img.freepik.com/premium-vector/vector-new-twitter-x-white-logo-black-background_744381-866.jpg" alt="HarshThakkar971" height="40" width="50" /></a>
  &nbsp;&nbsp;
  	<a href="https://linkedin.com/in/harsh-thakkar-7764bb1a4" target="blank"><img align="center" src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/ca/LinkedIn_logo_initials.png/800px-LinkedIn_logo_initials.png" alt="harsh-thakkar-7764bb1a4" height="40" width="40" /></a>
  &nbsp;&nbsp;
 <a href="https://instagram.com/harsh_thakkar09" target="blank"><img align="center" src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/e7/Instagram_logo_2016.svg/768px-Instagram_logo_2016.svg.png" alt="harsh_thakkar09" height="40" width="40" /></a>
</p>
