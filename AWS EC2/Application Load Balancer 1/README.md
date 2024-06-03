# AWS Application Load Balancer Project

## Project Overview

<img src="https://github.com/Harsh971/AWS-Projects/blob/main/AWS%20EC2/Application%20Load%20Balancer%201/architecture.png"></img>

This project demonstrates the use of an AWS Application Load Balancer (ALB) to distribute traffic across three EC2 instances. Each instance hosts a different `index.html` file. By refreshing the browser, we can see the content change, indicating that the load balancer is successfully distributing requests among the instances.

## Architecture Design

### AWS Components

1. **EC2 Instances**:
   - Three EC2 instances are created, each with a unique `index.html` file.
   - The instances are configured to serve these files via an HTTP server.

2. **Application Load Balancer (ALB)**:
   - An Application Load Balancer is set up to distribute incoming traffic across the three EC2 instances.
   - The ALB is configured to handle HTTP traffic on port 80.

3. **Security Groups**:
   - Security groups are created and associated with the EC2 instances and the ALB to control inbound and outbound traffic.
   - The security group for the instances allows HTTP (port 80) traffic from the ALB.
   - The security group for the ALB allows HTTP (port 80) traffic from the internet.

## Steps for Implementation

### Step 1: Launch EC2 Instances

1. Launch three EC2 instances using the AWS Management Console.
   - Choose an appropriate Amazon Machine Image (AMI) (e.g., Amazon Linux 2).
   - Select an instance type (e.g., t2.micro for free tier).
   - Configure instance details, storage, and add tags as needed.
   - Configure the security group to allow HTTP (port 80) and SSH (port 22) access.
   - Launch the instances and connect to each using SSH.

2. Install an HTTP server on each instance (e.g., Apache):
   ```sh
   sudo yum update -y
   sudo yum install -y httpd
   sudo systemctl start httpd
   sudo systemctl enable httpd
   ```

3. Create a unique `index.html` file on each instance:
   - On Instance 1:
     ```sh
     echo "<html><body><h1>Instance 1</h1></body></html>" | sudo tee /var/www/html/index.html
     ```
   - On Instance 2:
     ```sh
     echo "<html><body><h1>Instance 2</h1></body></html>" | sudo tee /var/www/html/index.html
     ```
   - On Instance 3:
     ```sh
     echo "<html><body><h1>Instance 3</h1></body></html>" | sudo tee /var/www/html/index.html
     ```

### Step 2: Configure the Application Load Balancer (ALB)

1. Navigate to the EC2 Dashboard and select "Load Balancers" from the left menu.
2. Click "Create Load Balancer" and choose "Application Load Balancer".
3. Configure the load balancer:
   - Name: `my-app-load-balancer`
   - Scheme: Internet-facing
   - IP address type: IPv4
   - Listeners: Add a listener for HTTP on port 80
   - Availability Zones: Select the VPC and availability zones where the EC2 instances are running.
4. Configure the security group for the load balancer to allow HTTP traffic from the internet.
5. Configure the target group:
   - Create a new target group for HTTP.
   - Register the three EC2 instances with this target group.
6. Review and create the load balancer.

### Step 3: Verify Load Balancer Configuration

1. Retrieve the DNS name of the load balancer from the AWS Management Console.
2. Open a web browser and navigate to the load balancer's DNS name.
3. Refresh the page multiple times to see the content from each `index.html` file, indicating that the load balancer is distributing traffic among the instances.

